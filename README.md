# Vagrant Configuration

The included Vagrantfile will allow you to get up and running with a development box quickly.

# Requirements

The following applications must already be installed:

1. Vagrant 1.6.5
2. VirtualBox

## Project Structure

A typical folder structure for a project would look like the following:

    ansible/
        .. Contents of <http://github.com/simoncoulton/ansible>
    secure/
        .. Secure files required for deployments (used by Ansible), should not be included in your repo.
    source/
        app/
        public/
            css/
            img/
            js/
    vagrant/
        .. Contents of this repo

## Customizing the VM

The Ansible repo provides a `vagrant` playbook and role to use when provisioning the VM. There are several things that must be setup in order to install the required applications:

1. Modify the group_vars.

PHP, uWSGI, Apache, Nginx, MySQL and PostreSQL roles are all run based upon the a configuration variable being set (php, uwsgi, apache, nginx, mysql, postgresql respectively). Simply set each one you want to install to True in your group_vars.

2. Create a `secure/vars/database.yml` and `secure/vars/web.yml` file. 
 
These will be used for specific secure settings that you want to keep outside of your repository.

3. Create the vagrant configuration

This will replace the VMs webserver virtualhost configuration with one designed specifically for the VM. Examples can be seen in <http://github.com/simoncoulton/ansible> under `roles/vagrant/defaults/main.yml`. Create the relevant config in the vagrant.yml *group_var*.

## Creating your first Vagrant box

Once you've created the above folder structure and cloned the relevant repositories, open your terminal, navigate to the folder, and enter `vagrant up`. This will begin the initialization process, creating the VM with Ubuntu 14.04 LTS, and provisioning it with the applications required (see Customizing the VM).

The `source/` folder will be mapped to `/var/www` with your webserver automatically pointing to `/var/www/public` as the root. The VM will be given a static IP address of *192.168.10.145* and a hostname of *dev*.



