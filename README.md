# NS Ubuntu Development Environment

Powered by [![Virtualbox](https://github.com/MartijnSips/ubuntu-development-environment/raw/develop/Logos/virtualbox.png "Virtualbox")](http://www.virtualbox.org), [![Vagrant](https://github.com/MartijnSips/ubuntu-development-environment/raw/develop/Logos/vagrant.png "Vagrant" )](http://www.vagrantup.com) and [![Ansible](https://github.com/MartijnSips/ubuntu-development-environment/raw/develop/Logos/ansible.png "Ansible")](http://www.ansible.com)

---

**NOTE**

The scripts in here are based on the [open source ubuntu development environment](https://github.com/martijnsips/ubuntu-development-environment).

---

## Purpose

The scripts in the directory are meant to give you a linux development environment to start your work on NS development.

The advantage of these scripts is that if all team members use this, then they will all have the same kind of image. Also, all stuff which would be helpfull for all members could be added to this repo, so that everybody gets this aswell.

## Getting started

In order to use these scripts, you need the following to be installed, although it might also work with the MacOS or Linux equivalents. That is not tested though.

- Windows 10
- Virtual Box ([https://www.virtualbox.org](https://www.virtualbox.org/))
- Vagrant ([https://www.vagrantup.com/](https://www.vagrantup.com/))

Then run the getlatestbaseimagescripts.cmd (only once) from a command prompt in this directory. This will download the default base image script files.

Appart from that you will need a ssh key (see [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (only the part on generating a new SSH key)) in order to create your ssh key. Then add it to your account on bitbucket/gitlab and/or azure devops. This is needed in order for Ansible to be able to download the repositories.

After that you can ```vagrant up``` this image.

---

**NOTE**

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

## NS Specific actions

At [NS Confluence](https://confluence.topaas.ns.nl/display/OBIST/01.00+-+Access+requirements) you can find the actions to do.

From a CGI point of view you will need to do the following things though:

- Get a billingcode
- Create a .ssh key
- Assign the .ssh public key to your accounts on bitbucket/gitlab and azure devops.
- Request a bypass for your pc for the noc.ns.nl url in order to get to the NS Noc VPN.
- Request a bypass for your pc for the azuregateway-00a60069-86d0-4e71-9118-f0bf61f4ec2b-6679dfe9e35e.vpn.azure.com url in order to be able to connect via the openvpn to the NS VPN (to be able to get to the jenkins server for example)
