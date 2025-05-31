proxmox-install-packages
=========

Created to automate the installation of packages on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device.

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
In your playbook, you should specify a vars_files:
```
  vars_files:  
   - vars/packages-vars.yml
```
This vars_files can be formated as this. Change the name of the packages, their state, and quantity in the array, based on your needs.
```
packages:
  - name: vim
    state: latest
  - name: nload
    state: latest
```
Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  vars_files:  
   - vars/packages-vars.yml
  roles:
  - proxmox-install-packages
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan