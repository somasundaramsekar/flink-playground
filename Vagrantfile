# -*- mode: ruby -*-
# vi: set ft=ruby :
 
# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"

  config.vm.define "slave1" do |machine|
    machine.vm.network "private_network", ip: "172.17.177.21"
    machine.vm.hostname = "slave1.local"
    machine.vm.provider "virtualbox" do |v|
      v.gui = false #true
      v.memory = 2000
      v.cpus = 2
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--vram", "16"]
    end
  end

  config.vm.define "slave2" do |machine|
    machine.vm.network "private_network", ip: "172.17.177.22"
    machine.vm.hostname = "slave2.local"
    machine.vm.provider "virtualbox" do |v|
      v.gui = false #true
      v.memory = 2000
      v.cpus = 2
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--vram", "16"]
    end
  end

  config.vm.define 'master' do |machine|
    machine.vm.network "private_network", ip: "172.17.177.11"
    machine.vm.hostname = "master.local"
    
    #https://github.com/mitchellh/vagrant/issues/6793
    machine.vm.provision "shell", inline: "sudo apt-get install -y python-pip python-dev && sudo pip install ansible==1.9.2 && sudo cp /usr/local/bin/ansible /usr/bin/ansible"


    machine.vm.provision :ansible_local do |ansible|
      ansible.playbook       = "ansible.yml"
      ansible.verbose        = true
      ansible.install        = true
      ansible.limit          = "all" # or only "nodes" group, etc.
      ansible.inventory_path = "inventory"
    end

    machine.vm.provider "virtualbox" do |v|
      v.gui = false #true
      v.memory = 2000
      v.cpus = 2
      v.customize ["modifyvm", :id, "--ioapic", "on"]
      v.customize ["modifyvm", :id, "--vram", "16"]
    end
  end


end