
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
	config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
	config.vm.synced_folder "./config", "/vagrant/config", mount_options: ["dmode=755,fmode=755"]
    config.vm.box = "ubuntu/bionic64"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
    end

	# Set slave first
    config.vm.define "mysqlslave",  do |machine1|
        machine1.vm.host_name = "mysqlslave.local"
		machine1.vm.synced_folder "./data/slave", "/var/lib/mysql_vagrant" , id: "mysql",
		owner: 108, group: 113,  # owner: "mysql", group: "mysql",
		mount_options: ["dmode=775,fmode=664"]
        machine1.vm.network "private_network", ip: "192.168.10.80"
        machine1.vm.provision "shell", inline: $useraddscript
        machine1.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
			vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
			vb.customize ["modifyvm", :id, "--name", "mysqlslave"]
        end
		machine1.vm.provision :shell, path: "bootstrap-slave.sh"
    end

    config.vm.define "mysqlmaster", do |machine2|
        machine2.vm.host_name = "mysqlmaster.local"
		machine2.vm.synced_folder "./data/master", "/var/lib/mysql_vagrant" , id: "mysql",
		owner: 108, group: 113,  # owner: "mysql", group: "mysql",
		mount_options: ["dmode=775,fmode=664"]
        machine2.vm.network "private_network", ip: "192.168.10.70"
        machine2.vm.provision "shell", inline: $useraddscript
        machine2.vm.provider "virtualbox" do |vb|
            vb.cpus = 1
			vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
			vb.customize ["modifyvm", :id, "--name", "mysqlmaster"]  
        end
		machine2.vm.provision :shell, path: "bootstrap-master.sh"
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