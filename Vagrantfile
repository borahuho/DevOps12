
$useraddscript = <<SCRIPT
useradd -m henk -s /bin/bash
groupadd operators
usermod -aG operators henk
mkdir /operators
chown henk /operators
chgrp operators /operators
SCRIPT


Vagrant.configure('2') do |config|
    
    # set default settings
    config.vm.box = "ubuntu/bionic64"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
    end

    config.vm.define "mysql1", primary: true do |machine1|
        machine1.vm.host_name = "mysql1.local"
        machine1.vm.network "private_network", ip: "192.168.10.70"
        machine1.vm.provision "shell", inline: $useraddscript
        machine1.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
        end
    end

    config.vm.define "mysql2", primary: false do |machine2|
        machine2.vm.host_name = "mysql2.local"
        machine2.vm.network "private_network", ip: "192.168.10.80"
        machine2.vm.provision "shell", inline: $useraddscript
        machine2.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
        end
    end

    config.vm.define "HAproxy2", primary: false do |machine3|
        machine3.vm.host_name = "HAproxy2.local"
        machine3.vm.network "private_network", ip: "192.168.10.90"
        machine3.vm.provision "shell", inline: $useraddscript
        machine3.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
        end
        machine3.vm.synced_folder "DevOps12/", "/home/vagrant/mission"
    end
end