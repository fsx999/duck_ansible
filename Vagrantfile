# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define "postgresql" do | postgresql |
    postgresql.vm.box_check_update = true
    postgresql.vm.box = "ubuntu/trusty64"
    postgresql.vm.network "forwarded_port", guest: 5432, host: 5433
    postgresql.vm.network "private_network", ip: "192.168.33.11"
#    postgresql.vm.provision "ansible" do |ansible|
#      ansible.playbook = "provisioning/postgresql.yml"
#      ansible.extra_vars = "provisioning/var.yml"
#      ansible.vault_password_file = "~/.vault_pass.txt"
#      ansible.skip_tags = 'install'
#    end
   postgresql.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     # Customize the amount of memory on the VM:
     vb.memory = "2048"
   end
  end

  config.vm.define "web", primary: true do | web |
    web.vm.box = "ubuntu/trusty64"
    web.vm.box_check_update = true
    web.vm.network "forwarded_port", guest: 8081, host: 8081
    web.vm.network "forwarded_port", guest: 443, host: 443
    web.vm.network "forwarded_port", guest: 80, host: 8085
    web.vm.network "forwarded_port", guest: 8082, host: 8082
    web.vm.network "forwarded_port", guest: 8083, host: 8083
    web.vm.network "forwarded_port", guest: 8084, host: 8084
    web.vm.network "private_network", ip: "192.168.33.10"
#    web.vm.synced_folder "../../PycharmProjects", "/home/vagrant/PycharmProjects"
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/web.yml"
      ansible.extra_vars = "provisioning/var.yml"
      ansible.vault_password_file = "~/.vault_pass.txt"
      ansible.tags="site_ied"
  #    ansible.skip_tags = 'update'
    end
     web.vm.provider "virtualbox" do |vb|
     # Display the VirtualBox GUI when booting the machine
     # Customize the amount of memory on the VM:
     vb.memory = "2048"
   end
  end
end
