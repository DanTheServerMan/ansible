proxmox-chronyc
=========

Created to automate the configuration of chronyc on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device.

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
```
ntp_servers:
  - name: 0.us.pool.ntp.org
timezone: 'UTC'
```
Note that iburst is defined statically in the Jinja template. If you don't want it, you can modify the template.


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
  - proxmox-chronyc
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan