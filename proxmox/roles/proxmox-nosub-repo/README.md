proxmox-nosub-repo
=========

Created to automate the configuration of non-subscription repositories on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device. 

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
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

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  roles:
  - proxmox-nosub-repo
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan