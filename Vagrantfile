# -*- mode: ruby -*-
# vi: set ft=ruby :
IMAGE_NAME = "generic/ubuntu1804"
N = 1
Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
    v.linked_clone = true
  end

  (1..N).each do |i|
    config.vm.define "controller-#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.disksize.size = '50GB'
      node.vm.network "private_network", ip: "10.240.0.#{i + 10}"
      node.vm.hostname = "controller-#{i}"
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "kubernetes-setup/cluster-setup.yaml"
        ansible.extra_vars = {
          node_name: "controller-#{i}",
          node_ip: "10.240.0.#{i + 10}",
          pod_network_cidr: "10.200.0.0/16",
          pods_cidr: "10.200.1#{i}.0/24",
          role: "controller",
          ansible_python_interpreter: "/usr/bin/python3",
        }
      end
    end
  end

  (0..2).each do |i|
    config.vm.define "worker-#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.disksize.size = '50GB'
      node.vm.network "private_network", ip: "10.240.0.#{i + 20}"
      node.vm.hostname = "worker-#{i}"
      node.vm.provision "ansible" do |ansible|
        ansible.playbook = "kubernetes-setup/cluster-setup.yaml"
        ansible.extra_vars = {
          node_name: "worker-#{i}",
          pod_network_cidr: "10.200.0.0/16",
          node_ip: "10.240.0.#{i + 20}",
          pods_cidr: "10.200.2#{i}.0/24",
          role: "worker",
          ansible_python_interpreter: "/usr/bin/python3",
        }
      end
    end
  end
end
