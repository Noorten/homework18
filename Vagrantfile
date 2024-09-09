# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Общие параметры для всех ВМ
  config.vm.box = "ubuntu/bionic64"

  # Backup server configuration
  config.vm.define "backup" do |backup|
    backup.vm.hostname = "backup"
    backup.vm.network "private_network", ip: "192.168.56.15"
    
    backup.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end

    backup.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "inventory"
      ansible.groups = {
        "backup" => ["backup"],
      }
    end
  end

  # Client server configuration
  config.vm.define "client" do |client|
    client.vm.hostname = "client"
    client.vm.network "private_network", ip: "192.168.56.10"
    
    client.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end

    client.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "inventory"
      ansible.groups = {
        "client" => ["client"],
      }
    end
  end
end
