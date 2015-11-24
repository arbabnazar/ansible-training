# Ansible Training
[Ansible](http://docs.ansible.com/ansible/) is a configuration management tool that allows you to configure and manage other machines remotely. What makes it unique from other configuration management software like Chef or Puppet:

- It uses existing SSH infrastructure
- No needs for dedicated server, even your laptop can management 100s of machine
- Easy to get started with it
- It uses "Facts", gathers information about system and environment before running the tasks
- Ansible Tasks are idempotent

Prerequisites for Training:
------------------------------
You need the install the following software on your machine:

 1 - [Vitualbox](https://www.virtualbox.org/wiki/Downloads)

 2 - [Vagrant](https://www.vagrantup.com)

Cloning the tutorial
-----------------------
```shell
git clone https://github.com/arbabnazar/ansible-training.git
cd ansible-training
```
This training already contains a `Vagrantfile` to get you up and running. Note that you do not need to download any "box" manually. Just run this command and it will get everything for you that you need to perform this training.
```shell
vagrant up
```
It will bring up the **control** machine (Ubuntu 14.04 LTS) and perform the following actions on it:
- Add the latest  Ansible repository
- Add the insecure RSA key that will be used for client machines
- Add some additional SSH config

Once your machine is up and running, login to the control machine using the following command:
```
vagrant ssh
```
There are two other machines, which will be used as clients for practice, on which we'll perform the  configuration using ansible from *control* machine, given them the named 
. web
. database

To start these machines, use the following commands:
```
vagrant up web
vagrant up database
```
If something will go wrong, please refer to the Vagrant's [Getting Started Guide](http://docs.vagrantup.com/v2/getting-started/index.html).

For  grammar, spelling mistake etc... please create a PR for the master branch directly.

Thank you!
