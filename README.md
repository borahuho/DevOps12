# DevOps12

With this vagrant, you will install 3 Ubuntu 18.04 machines, 2x MySQL servers and 1 ubuntu server for HAproxy.
It will add some default users, groups and directory's. First you have to set up the MySQL master to master nodes and then the HAproxy server.
This Vagrant is to practice with MySQL and HAproxy.
This repository is intended for educational purpose only.


## Prerequisites

Works on Windows 10 and tested on macOS (macOS needs the Virtualbox extension pack).

Software needed:
* Virtualbox 5.0 or higher
* Git bash for Windows
* Vagrant 2.2.6 or higher


## Demo installation && use Vagrant

Youtube: https://youtu.be/KABnIuaA8SM


## Demo MySQL Master nodes and HAproxy

Youtube: 


## Installation

* Install Virtualbox: https://www.virtualbox.org/wiki/Downloads
* Install Git bash for Windows: https://gitforwindows.org/
* Install Vagrant for Windows: https://www.vagrantup.com/downloads.html

## Run this Vagrant VM
Open **Git Bash** in Windows
```
cd Documents
mkdir vagrant && cd vagrant
git clone https://github.com/borahuho/DevOps12
cd DevOps12
vagrant up
vagrant ssh HAproxy
```
## Mission

Read your mission in ~/vagrant/mission (on HAproxy server)

## Network
Vagrant VM will be set up with 2 network adapters
```
Nat : DHCP
Localhost (mysql1): 192.168.10.70

Nat : DHCP
Localhost (mysql2): 192.168.10.80

Nat : DHCP
Localhost (HAproxy2): 192.168.10.90
```
## Vagrant commands
Start VM's with Vagrant
```
vagrant up
```
Stop and shutdown a VM
```
vagrant halt
```
Remove a VM
```
vagrant destroy
```
ssh in to the VM
```
vagrant ssh mysql1
vagrant ssh mysql2
vagrant ssh HAproxy2
```

