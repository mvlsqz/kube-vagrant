# kube-vagrant
Kubernetes running on vagrant, for testing porpouses 

# Requirements
* Python virtual environment manager, [Miniconda](https://www.google.com) will be used to run this example
* VirtualBox
* Vagrant
* Vagrant disk resize plugin `vagrant plugin install vagrant-disksize`

# Preparing workspace
Installing virtual environment
```bash
conda create -n kube-vagrant python=2
```
Activating virtual environment
```bash
conda activate kube-vagrant
```
Clone this repo
```bash
git clone https://github.com/mvlsqz/kube-vagrant.git
```
Bring up the cluster
```bash
cd kube-vagrant && vagrant up
```
Once vagrant/ansible are done with its job you can ssh to the `controller-1` node to start play with your cluster
````bash
vagrant ssh controller-1
