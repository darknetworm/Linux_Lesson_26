# -*- mode: ruby -*-
# vim: set ft=ruby :
#export VAGRANT_EXPERIMENTAL="disks"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end
  config.vm.define "client" do |bkpcli|
    bkpcli.vm.network "private_network", ip: "192.168.56.11", virtualbox__intnet: "vboxnet0"
    bkpcli.vm.hostname = "client"
  end
  config.vm.define "server" do |bkpsrv|
    bkpsrv.vm.network "private_network", ip: "192.168.56.10", virtualbox__intnet: "vboxnet0"
    bkpsrv.vm.hostname = "server"
    bkpsrv.vm.disk :disk, size: "2GB", name: "backup_disk"
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "main.yml"
    ansible.inventory_path = "hosts"
  end
end
