# rabbitmq-cluster
Clustering RabbitMQ with Ansible

## What is it?

Ansible playbook and vagrant development environment for installing a RabbitMQ broker cluster across N many nodes.

## Getting Started

```
brew cask install virtualbox
brew cask install vagrant
vagrant plugin install vagrant-hostmanager
vboxmanage hostonlyif create
vboxmanage hostonlyif ipconfig vboxnet0 --ip 10.125.0.1 --netmask 255.255.255.0
vboxmanage dhcpserver remove --ifname vboxnet0
vagrant up
```

This repository is derived mainly from [this article](https://github.com/rochfordk/OpenStack-HA/wiki/Clustered-RabbitMQ-test-deployment-instructions).
