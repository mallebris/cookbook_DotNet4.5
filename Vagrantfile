# -*- mode: ruby -*-
# vi: set ft=ruby :
hostname = 'winEnv.local'
VAGRANTFILE_API_VERSION = "2"
VAGRANT_LOG = 'debug'
Vagrant.require_version ">= 1.7.0"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = hostname
  config.vm.box = "Win32"
  config.vm.communicator = "winrm"
  config.vm.provision "shell", path: "install.cmd"
  config.vm.network :private_network, ip: "33.33.33.10"
  config.vm.network "public_network"
  config.vm.guest = :windows
  config.vm.network :forwarded_port, guest: 3389, host: 3389, id: "rdp", auto_correct: true
  config.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true

  config.winrm.username = "vagrant"
  config.winrm.password = "vagrant"

  config.omnibus.chef_version = :latest
  config.berkshelf.berksfile_path = "./Berksfile"
  config.berkshelf.enabled = true
  
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    vb.memory = "1024"
  end

  config.vm.provision :chef_solo do |chef|
    chef.json = {
      'NetFramework' => {
        'version' => :latest
      }
    }
    chef.add_recipe("NetFramework")
  end
end
