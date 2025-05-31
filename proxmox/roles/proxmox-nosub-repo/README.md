proxmox-nosub-repo
=========

Created to automate the configuration of NFS storage on ProxMox in my homelab.

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
pve_enterprise_repo: 
ceph_enterprise_repo: 
pve_nosub_repo: 
ceph_nosub_repo: 
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