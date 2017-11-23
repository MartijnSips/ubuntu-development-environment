# Linux development environment

## Purpose

The purpose of these scripts are to easily create an Linux development environment
which you can simply roll out.

These scripts will create an Ubuntu Mate 16.04 development image with the following products installed:

- IntellIJ (latest)
- Eclipse Oxygen- SoapUI
- Postgresql 9.5
- PHP
- ActiveMQ 5.15.0
- Atom
- Git
- Gitkraken
- Maven
- Tomcat
- Visual Studio Code

The advantage of having these scripts, is that you can destroy your image and deploy your image again if you have broken something.
The other thing is that in a team, all members have the same image, thus the same structure.

## Requirements/Tested on

In order to use these scripts, you need the following to be installed, altough it might also work with the MacOS or Linux equivalents. That is not tested though.

- Windows 10
- Virtual Box 5.2
- Vagrant 2.0.0

## How to create a new environment

First download this repository to a directory of your choosing on your host.

Then in a command line in that directory execute the following command in this directory:

```vagrant up```

This will start the creation of your personal local Ubuntu Mate development environment.

Each time after you have shut down the image execute the following command:

```vagrant reload```

This last command will make sure that the directory mappings are also loaded.

## How this all works

The Vagrantfile is the starting point for the `vagrant up` command. In that file is defined which base image vagrant should
use to download.
When that base image is downloaded it will only look whether it is the latest version if you run the `vagrant up`
command again.

Then vagrant will create an virtualbox image based on that (only once downloaded) base image and the specification in
the vagrantfile.

When the virtualbox image is created it will start the provisioning, also specified in the vagrant file.
This will first update all packages on the image, and then trigger the development.yml playbook in the ansible
directory.

That development.yml playbook will then install all required packages needed for general linux development.