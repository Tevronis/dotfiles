#vagrant
# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vagrant.plugins = "vagrant-disksize"

  config.vm.box = "ubuntu/bionic64"

  config.disksize.size = "60GB"

  config.vm.synced_folder ".", "/vagrant" #, type: "nfs"
  config.vm.synced_folder "../aos-web-ui", "/opt/aos-web-ui" #, type: "nfs"
  config.vm.synced_folder "../systest", "/opt/systest" #, type: "nfs"

  config.vm.network "forwarded_port", guest: 8888, host: 8847
  config.vm.network "private_network", ip: "55.55.55.5"

  config.vm.provision "shell", inline: <<-EOS
    /vagrant/vagrant_vm_setup.sh
  EOS
# Enable Dynamic Swap Space to prevent Out of Memory crashes
  # config.vm.provision "shell", inline: "sudo apt install swapspace -y"
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--cpus", "4"]
    vb.customize ["modifyvm", :id, "--memory", "4592"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end
end
