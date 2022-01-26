# Linux Development Environment

Powered by [![Virtualbox](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/virtualbox.png "Virtualbox")](http://www.virtualbox.org),
[![Vagrant](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/vagrant.png "Vagrant" )](http://www.vagrantup.com)
and [![Ansible](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/develop/Logos/ansible.png "Ansible")](http://www.ansible.com)

## Purpose

The purpose of these scripts are to easily create an Linux development environment which you can simply roll out multiple times and get the same image. Ready to start developing your projects.

These scripts will create an Ubuntu 21.10 development image (updated with all latest patches). Refer to Ansible/development.yml to see what packages are installed.

The advantage of having these scripts, is that you can destroy your image and deploy your image again if you have broken something. The other thing is that in a team, all members have the same image with the same settings, thus the same structure. Your code will work the same on each image.

## Getting started

In order to use these scripts, you need the following to be installed, although it might also work with the MacOS or Linux equivalents. That is not tested though.

- Windows 10
- Virtual Box ([https://www.virtualbox.org](https://www.virtualbox.org/))
- Vagrant ([https://www.vagrantup.com/](https://www.vagrantup.com/))

Then run the getlatestbaseimagescripts.cmd (only once) from a command prompt in this directory. This will download the default base image files.

Appart from that you will need a ssh key (see [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (only the part on generating a new SSH key)) in order to create your ssh key. Then add it to your account on bitbucket/gitlab and/or azure devops. This is needed in order for Ansible to be able to download the repositories.

After that you can ```vagrant up``` this image.

---

**Note** Before you start, please make sure that you are **not** on a VPN connection. A VPN connection might restrict your internet access, and because this repo uses several internet packages it might fail.

---

First download the "Example Project Specific Development Environment" directory from this repository to a directory of your choosing on your host.

Follow the instructions in the README.md of that project.

## How does it work?

The Vagrantfile is the starting point for the `vagrant up` command. In that file is defined which base image vagrant should
use to download.
When that base image is downloaded it will only look whether it is the latest version if you run the `vagrant up`
command again.

Then vagrant will create an virtualbox image based on that (only once downloaded) base image and the specification in
the vagrantfile. Hyper-V or parallels can also be configured but this is not tested or implemented.

When the virtualbox image is created it will start the provisioning, also specified in the vagrant file.
This will first update all packages on the image, and then trigger the development.yml playbook in the ansible
directory.

That development.yml playbook will then install all required packages needed for general linux development.

### Vagrantfile

#### Host directory

### Vagrantfile.user.sample

The Vagrantfile.user.sample is an example file where we can specify your specific custom configuration, like your preferred ide 
installation, background image or other specific windows settings.  
Also, your own public ssh keys for example can be created in this file.

Before you can use this copy it to Vagrantfile.user 

### Vagrantfile.project.sample

The Vagrantfile.project is the place where we can specify our project specific things to be downloaded.
For example all git repositories needed for this project. 

Before you can use this copy it to Vagrantfile.project