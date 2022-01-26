# Example Project Linux Development Environment

Powered by [![Virtualbox](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/virtualbox.png "Virtualbox")](http://www.virtualbox.org),
[![Vagrant](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/vagrant.png "Vagrant" )](http://www.vagrantup.com)
and [![Ansible](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/ansible.png "Ansible")](http://www.ansible.com)

<b>Note</b>: The scripts in here are based on the [open source ubuntu development environment](https://github.com/martijnsips/ubuntu-development-environment).

## Purpose

The scripts in the directory are mean to give you a linux development environment for your own project.

## Getting started

In order to use these scripts, you need the following to be installed, although it might also work with the MacOS or Linux equivalents. That is not tested though.

- Windows 10 (or MacOS or Linux)
- Virtual Box ([https://www.virtualbox.org](https://www.virtualbox.org/))
- Vagrant ([https://www.vagrantup.com/](https://www.vagrantup.com/))

Download this directory to your local machine. Then adjust the Vagrantfile.project and Vagrantfile.user with your project and own specific configuration.

Then run the getlatestbaseimagescripts.ps1 (or .sh) from a command prompt in this directory. This will download the 
default base image files.

---

Note: In case if you want to use the getlatestbaseimagescripts.ps1, you need to open a powershell prompt first and then type ```Set-ExecutionPolicy -ExecutionPolicy unrestricted``` only once. This will allow powershell to execute scripts.

---

Apart from that you will need a ssh key (see [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (only the part on generating a new SSH key)) in order to create your ssh key. Then add it to your account on your repository application like github, bitbucket or VSTS. This is needed in order for Ansible to be able to download the repositories.

After that you can ```vagrant up``` this image to get a specific environment for your project. This would take about 40-50 minutes normally. Depending on what additional things you install for your project.

---

NOTE

If you get some certificate warnings while vagrant tries to install the plugins, try this first:

```cmd
vagrant plugin install vagrant-vbguest --plugin-clean-sources --plugin-source `http://rubygems.org`
vagrant plugin install vagrant-reload --plugin-clean-sources --plugin-source `http://rubygems.org`
vagrant up
```

---

If you want to reset your image you can than easily do

```cmd
vagrant destroy -f
```

to destroy the image and then

```cmd
vagrant up
```

to set it up again.

When something failed, you can continue the provisioning with the following command:"

```cmd
vagrant up --provision
```

