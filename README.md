# Ansible-DigitalOcean-Ubuntu Bootstrapper

This [Ansible](http://ansible.com) playbook will allow you to bootstrap an [Ubuntu](http://ubuntu.com) server that has just been created in [DigitalOcean](http://digitalocean.com).

Bootstrapping is necessary because a newly provisioned Ubuntu image on DigitalOcean will only have the ``root`` user available for login.  While that's nice and all, it's bad security to allow logins from this account.  Instead, what should happen is the server should disallow ``root`` logins, and delegate ``sudo`` privileges to an operations account.

I kept having to manually bootstrap my DigitalOcean VMs before I could start using my project-specific configuration and deployment Ansible scripts, so I finally made this utility to automate the process.

**WARNING: Once this playbook runs successfully on your target server, it will not work a second time because the ``root`` user will now be locked out.**

## Requirements

* POSIX-style system
* Ansible
* A DigitalOcean account
* A working knowledge of Ansible
* A sense of humour
* [SSH keys set on your DigitalOcean account](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets)

## Getting Started

* [Install Ansible](http://docs.ansible.com/intro_installation.html)
* Clone this repository
* Add an inventory file for your machine(s)
* (Optional) Modify any variable in a ``group_vars`` file

## What it Does

* Logs into the target machine(s) using an SSH
* Creates an operations account (with SSH keys and a random password)
* Adds your local SSH public key to the operations account ``authorized_keys`` file
* Disallows logins from the ``root`` account

Once this playbook finishes, you can SSH into the operations account using your SSH keys.

