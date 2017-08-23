# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# A Vagrantfile to generate a VM with an empty postgresql installation.
# Useful for testing backup restores.
# Forked from https://github.com/jackdb/pg-app-dev-vm
# 

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: $script
  config.vm.synced_folder "src/", "/srv/src"
end

Vagrant::Config.run do |config|
  config.vm.box = "debian/jessie64"
  config.vm.box_url = "https://app.vagrantup.com/debian/boxes/jessie64"
  config.vm.host_name = "postgresql" 

  config.vm.share_folder "bootstrap", "/mnt/bootstrap", ".", :create => true
  config.vm.provision :shell, :path => "Vagrant-setup/bootstrap.sh"
  
  # PostgreSQL Server port forwarding
  config.vm.forward_port 5432, 15432
end
