proxmox-nosub-repo
=========

Created to automate the configuration of non-subscription repositories on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device. 

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
In your playbook, you should specify a vars_files:
```
  vars_files:  
   - vars/repo-vars.yml
```
This vars_files can be formated as this. Change the name of the packages, their state, and quantity in the array, based on your needs.
```
disable_repository:
  - repo: deb https://enterprise.proxmox.com/debian/ceph-squid bookworm enterprise
  - repo: deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
enable_repository:
  - repo: deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
  - repo: deb http://download.proxmox.com/debian/ceph-quincy bookworm no-subscription
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
   - vars/repo-vars.yml
  roles:
  - proxmox-nosub-repo
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan