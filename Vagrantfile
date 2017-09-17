# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

	unless Vagrant.has_plugin?("vagrant-vbguest")
	  raise 'vbguest plugin missing, install by using "vagrant plugin install vagrant-vbguest"'
	end

	unless Vagrant.has_plugin?("vagrant-reload")
	  raise 'reload plugin missing, install by using "vagrant plugin install vagrant-reload"'
	end

	# Guest additions plugin config
	config.vbguest.auto_update = true
	config.vbguest.no_remote = false

	config.vm.box = "cxtlabs/vagrant-ubuntu-16.04-mate"

	config.vm.provider "virtualbox" do |vb|
		vb.name = "Linux Development"
		vb.gui = true
		vb.cpus = "4"
		vb.memory = "8192"

		# Disable 3d acceleration because some programs crash on it.
		vb.customize ["modifyvm", :id, "--accelerate3d", "off"]

        # Enabling copy/paste to/from VM         
        vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
        vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
		
		# Add cdrom
        vb.customize ["storageattach", :id, "--storagectl", "IDE Controller", "--port", "0", "--device", "0", "--type", "dvddrive", "--medium", "emptydrive"]
	end
	
    config.vm.provision :reload

	config.vm.synced_folder "#{ENV['USERPROFILE']}\\Documents", '/home/vagrant/Documents', owner: "vagrant", group: "vagrant", create: true
	config.vm.synced_folder "#{ENV['USERPROFILE']}\\Downloads", '/home/vagrant/Downloads', owner: "vagrant", group: "vagrant", create: true

	config.vm.synced_folder "Ansible", '/home/vagrant/Ansible', create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]
	config.vm.synced_folder "Projects", '/home/vagrant/Projects', create: true, owner: "vagrant", group: "vagrant", mount_options: ["dmode=775,fmode=664"]

	config.vm.provision 'shell', inline: 'apt-get update'
	config.vm.provision 'shell', inline: 'apt-get install -y software-properties-common'
	config.vm.provision 'shell', inline: 'apt-add-repository ppa:ansible/ansible'
	config.vm.provision 'shell', inline: 'apt-get update'
	config.vm.provision 'shell', inline: 'apt-get install -y ansible'
	config.vm.provision 'shell', inline: 'cd /home/vagrant/Ansible && ansible-playbook -i inventory development.yml'
	
	config.vm.provision "shell", inline: "echo reloading ..."
    config.vm.provision :reload

	config.vm.provision "shell", inline: "echo loading custom vagrant ..."
	# Load custom vagrant file it it exists.
	client_vagrantfile = File.expand_path('./Vagrantfile.client', __FILE__)
	load client_vagrantfile if File.exists?(client_vagrantfile)

	config.vm.provision "shell", inline: "echo provisiong some user specificc shellscript ..."
	# Provision some user specific settings/configuration/packages
	user_config_file=".user-dev-box.sh"
	if File.file?(File.join(Dir.home, user_config_file))
        config.vm.provision "shell", path: File.join(Dir.home, user_config_file)
	end

	config.vm.provision "shell", inline: "echo done ..."
end

# Load custom vagrant file it it exists.
client_vagrantfile = File.expand_path('Vagrantfile.client', __FILE__)
load client_vagrantfile if File.exists?(client_vagrantfile)