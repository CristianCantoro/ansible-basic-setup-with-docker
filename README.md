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


## Credits

This playbook was inspired by Jeff Geerling's [`ìnternet-pi`](https://github.com/geerlingguy/internet-pi).
