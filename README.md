# Linux development environment [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) [![Maintainability](https://api.codeclimate.com/v1/badges/db516f2f06ec4ff978dd/maintainability)](https://codeclimate.com/github/MartijnSips/ubuntu-development-environment/maintainability) [![Build Status](https://travis-ci.org/MartijnSips/ubuntu-development-environment.svg?branch=development)](https://travis-ci.org/MartijnSips/ubuntu-development-environment)


Powered by [![Virtualbox](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/development/Logos/virtualbox.png "Virtualbox")](http://www.virtualbox.org),
[![Vagrant](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/development/Logos/vagrant.png "Vagrant" )](http://www.vagrantup.com)
and [![Ansible](https://raw.githubusercontent.com/MartijnSips/ubuntu-development-environment/development/Logos/ansible.png "Ansible")](http://www.ansible.com)

## Purpose

The purpose of these scripts are to easily create an Linux development environment
which you can simply roll out multiple times and get the same image. Ready to start developing your projects.

These scripts will create an Ubuntu Mate 16.04 development image (updated with all latest patches) and with at least the 
following products installed:

- IntellIJ (latest)
- Eclipse Oxygen- SoapUI
- Visual Studio Code
- Postgresql
- PHP
- ActiveMQ
- Atom
- Git
- Gitkraken
- Maven
- Tomcat
- Postman

The advantage of having these scripts, is that you can destroy your image and deploy your image again if you have broken 
something. The other thing is that in a team, all members have the same image with the same settings, thus the same 
structure. Your code will work the same on each image.

## Requirements

In order to use these scripts, you need the following to be installed, although it might also work with the MacOS or 
Linux equivalents. That is not tested though.

- Windows 10
- Virtual Box ([https://www.virtualbox.org](https://www.virtualbox.org/))
- Vagrant ([https://www.vagrantup.com/](https://www.vagrantup.com/))
- Git ([https://git-scm.com](https://git-scm.com/))

## How to create a new environment

First download this repository to a directory of your choosing on your host.

Then in a command prompt in that directory, execute the following command in this directory:

```vagrant up```

This will start the creation of your personal local Ubuntu Mate development environment.

Each time after you have shutdown the image execute the following command:

```vagrant reload```

This last command will make sure that the directory mappings are also loaded.

If you want to reset your image do the following:

```vagrant destroy```

and then

```vagrant up```

<b>Note:</b> On your image the Host directory is mounted in /home/vagrant/Host. This means that if you want to keep some
files when you are going to reset your image, you can copy them in that directory and you will find them there again 
when you have reset your image from your host.

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