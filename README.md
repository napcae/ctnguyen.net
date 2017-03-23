# Boostrapping and securing debian/jessie64(8) server for ctnguyen.net

This repository contains [Ansible](http://ansible.com) scripts for bootstrapping and securing the Debian server.

The included tasks are following:

* Update and upgrade Debian packages via aptitude
* Configure locale
* Install ntp to synchronize time
* Install optional packages defined in group vars
* Install fail2ban to block ssh brute-force attempts
* Delete root password
* Lock down sudo
* Lock down ssh to prevent root and password login
* Configure unattended security upgrades
* Create users

## Requirements

ansible 2.1.0.0

## Prerequisites

Create admin user and add this user to sudoers group.

```
$ ansible-playbook user.yml --user root

Enter username: napcae
Enter password: 
confirm Enter password: 
Enter id_rsa.pub path [~/.ssh/id_rsa.pub]: 
Add user to sudoers group (y/n) [n]: y
```

## Script execution

Finally, execute bootstrap Ansible task for admin user:

```
$ ansible-playbook bootstrap.yml --ask-become-pass -u napcae
sudo password:
```

## Reboot

After successfully bootstrapping and securing your server, reboot server for kernel updates.

```
$ ansible-playbook reboot.yml --ask-sudo-pass
sudo password: 
Are you sure you want to reboot server (yes/no)? [no]: yes
```

## Users

You can add new user or update the existing one using the following script:

```
$ ansible-playbook user.yml
```

## Firewall

iptables-persistent package

# Development

ansible-playbook bootstrap.yml  -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory
