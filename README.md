# vagrant-golang-ubuntu

Vagrant-based golang development environment using [Lubuntu](http://lubuntu.net/), with GUI (i.e., not headless).

The Vagrant base box is a minimal (~600 MB) Lubuntu 14.04 64-bit installation, [available from Atlas](https://atlas.hashicorp.com/halvards/boxes/lubuntu64).

## Installation

Prerequisites:

* [VirtualBox](https://www.virtualbox.org/wiki/Downloads), at least version 4.3.28
* [Vagrant](https://vagrantup.com/downloads.html). This has been tested using version 1.7.4
* [Ansible](https://github.com/ansible/ansible). This has been tested using version 1.9.2

Clone this repository, then from the repository folder run this command:

    vagrant up

The `vagrant` user password is `vagrant`.

## Notes

* The Vagrantfile assumes a directory called `~/golang`, which will be shared with the VM.
* The login form appears twice after the VM has been created the first time. On subsequent reboots, it only appears once.
* The Vagrantfile copies your private key to the VM so you can access Github et al. via SSH. It assumes the private key file can be found in `~/.ssh/id_rsa`
* You can also SSH to the VM, using `vagrant ssh`
* Only Mac OS X and Linux hosts are supported. See [this example](https://github.com/halvards/vagrant-vm/blob/ansible/nodejs-ubuntu64/Vagrantfile) for a Windows host workaround.

