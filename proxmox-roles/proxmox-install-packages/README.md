proxmox-install-packages
=========

Created to automate the installation of packages on ProxMox that are not included in the default installation. In my example, I prefer using vim as a text editor, so this script installs it.

Requirements
------------

- A ProxMox installation with network connectivity to your device.
- This role was developed targeting PVE 9.0.6.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
```
packages:
  - name: vim
    state: latest
  - name: nload
    state: latest
```
Change the name of the packages, their state, and quantity in the array, based on your needs.

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  roles:
  - proxmox-install-packages
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan