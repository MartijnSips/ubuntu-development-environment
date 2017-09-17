# Ubuntu Mate development environment

## Purpose

The purpose of these scripts are to easily create an linux development environment
which you can simply roll out.

These scripts will create an Ubuntu Mate 16.04 development image with the following products installed:

- IntellIJ (latest)
- Eclipse Oxygen
- SoapUI
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
- Virtual Box 5.1.26
- Vagrant 1.9.5

## How to create a new environment

First download this repository to a directory of your choosing on your host.

Then in a command line in that directory execute the following command in this directory:

```vagrant up```

This will start the creation of your personal local Ubuntu Mate development environment.

Each time after you have shut down the image execute the following command:

```vagrant reload```

This last command will make sure that the directory mappings are also loaded.

## How this repository is set up

tbd

