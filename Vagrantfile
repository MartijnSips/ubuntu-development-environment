# -*- mode: ruby -*-
# vi: set ft=ruby :

def install_missing_plugins(plugins_to_install:)
  plugins_to_install.select! { |plugin| not Vagrant.has_plugin? plugin }
  puts "Missing plugins are: #{plugins_to_install}" unless plugins_to_install.empty?
  plugins_to_install.each { |plugin|
    if system "vagrant plugin install #{plugin}"
      exec "vagrant #{ARGV.join(' ')}"
    else
      abort "Installation of plugin #{plugin} has failed. Aborting."
    end
  }
end

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  required_plugins = %w(vagrant-reload vagrant-vbguest)
  install_missing_plugins(plugins_to_install: required_plugins)

  # Guest additions plugin config
  config.vbguest.auto_update = false
  config.vbguest.no_remote = false

  # This is the base image which Vagrant should use to create a new virtual machine in virtualbox.
  config.vm.box = "cxtlabs/vagrant-ubuntu-16.04-mate"

  # Virtualbox specific configuration
  config.vm.provider "virtualbox" do |vb|
    vb.name = "Ubuntu Development Environment"
    vb.gui = true
    vb.cpus = "2"
    vb.memory = "4096"

    # Disable 3d acceleration because some programs crash on it.
    vb.customize ["modifyvm", :id, "--accelerate3d", "off"]

    # Enabling copy/paste to/from VM
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
		
    # Add cdrom
    vb.customize ["storageattach", :id, "--storagectl", "IDE Controller", "--port", "0", "--device", "0", "--type", "dvddrive", "--medium", "emptydrive"]
  end
	
  config.vm.provision "shell", inline: 'echo \>\>\> Reloading ...'
  config.vm.provision :reload

  config.vm.provision "shell", inline: 'echo \>\>\> Upgrading all packages ...'
  config.vm.provision 'shell', inline: 'apt update'

  config.vm.provision "shell", inline: 'echo \>\>\> Fix for grub ...'
  config.vm.provision 'shell', inline: 'DEBIAN_FRONTEND=noninteractive apt -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" upgrade'
  config.vm.provision 'shell', inline: 'apt-add-repository ppa:yannubuntu/boot-repair'
  config.vm.provision 'shell', inline: 'apt update'

  config.vm.provision 'shell', inline: 'apt install -y boot-repair'
  config.vm.provision 'shell', inline: 'boot-repair'

  config.vm.provision "shell", inline: 'echo \>\>\> Installing virtualbox guest additions ...'
  config.vm.provision 'shell', inline: 'DEBIAN_FRONTEND=noninteractive apt -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install virtualbox-guest-dkms virtualbox-guest-x11 linux-headers-$(uname -r)'

  # Mount the directories we need.
  config.vm.synced_folder "#{ENV['USERPROFILE']}\\Documents", '/home/vagrant/Documents', owner: "vagrant", group: "vagrant", create: true
  config.vm.synced_folder "#{ENV['USERPROFILE']}\\Downloads", '/home/vagrant/Downloads', owner: "vagrant", group: "vagrant", create: true
  config.vm.synced_folder "Ansible", '/home/vagrant/Ansible', create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
  config.vm.synced_folder "Host", '/home/vagrant/Host', create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]

  config.vm.provision "shell", inline: 'echo \>\>\> Running ansible scripts to install all other stuff ...'
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "Ansible/development.yml"
    # This loop wil also install/upgrade Ansible to latest
    ansible.version = "latest"
    # For debugging
    #ansible.verbose ="v"
  end

  config.vm.provision "shell", inline: "echo done ..."
end

# Load the file with user specific stuff
user_vagrantfile = File.expand_path('../Vagrantfile.user', __FILE__)
load user_vagrantfile if File.exists?(user_vagrantfile)

# Load the file with project specific stuff
project_vagrantfile = File.expand_path('../Vagrantfile.project', __FILE__)
load project_vagrantfile if File.exists?(project_vagrantfile)
