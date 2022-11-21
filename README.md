# Ansible Basic Setup with Docker

This is an ansible playbook to setup a new machine with Docker.

Most of the task are separated into roles that could be split from this
repository, but I still have to figure out how to organize everything so that
it is easily reusable.

## Workflow

1. Basic setup:
   - Enable locales (role: `locales`).
   - Upgrade system (role: `upgrade-release`).
   - Install basic packages (role: `install-basics`).

2. Install Docker (role: [`nickjj.docker`](https://github.com/nickjj/ansible-docker)).

## Usage

0. You can launch ansible from your machine or directly on the server, either way you need to install ansible in one place or the other. If you have an Ubuntu machine this consists in doing the following:
```
$ sudo apt update

$ sudo apt install software-properties-common

$ sudo add-apt-repository --yes --update ppa:ansible/ansible

$ sudo apt install ansible
```
otherwise refer to the [official Ansible documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

1. clone the repo and enter the repo root directory:
```
$ git clone https://github.com/CristianCantoro/ansible-basic-setup-with-docker

$ cd ansible-basic-setup-with-docker
```

2. install Ansible's requirements
```
$ ansible-galaxy install -r requirements.yml
```

3. (a) if you are on the server that you want to setup, copy the file `example.inventory.ini` to `inventory.ini` and change the configuration uncommenting the line to run the playbook locally and commenting the other.
```
$ cp example.inventory.ini inventory.ini

$ editor inventory.ini
[change as needed]

$ cat inventory.ini
[servers]
# 10.0.100.52 ansible_user=ubuntu

# Comment out the previous line and uncomment this to run locally.
127.0.0.1 ansible_connection=local ansible_user=ubuntu
```

3. (b) if you want to run the playbook from your machine, copy the file `example.inventory.ini` to `inventory.ini` and change the configuration to put the remote server address.
```
$ cp example.inventory.ini inventory.ini

$ editor inventory.ini
[change as needed]

$ cat inventory.ini
[servers]
xxx.xxx.xxx.xxx ansible_user=ubuntu

# Comment out the previous line and uncomment this to run locally.
# 127.0.0.1 ansible_connection=local ansible_user=ubuntu
```

Congrats, you have succesfully run the playbook!

## TODO

1. The `install-volume` role is not used at the moment and it is still incomplete. Its function would be to initialize and mount permanently - i.e. adding the needed configuration in `/etc/fstab` a new volume (e.g. /dev/sdb).

2. Add a script for adding new users to the system.

## Credits

This playbook was inspired by Jeff Geerling's [`ìnternet-pi`](https://github.com/geerlingguy/internet-pi).
