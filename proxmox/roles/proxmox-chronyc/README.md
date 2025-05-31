proxmox-chronyc
=========

Created to automate the configuration of chronyc on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device.

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
In your playbook, you should specify a vars_files:
```
  vars_files:  
   - vars/chronyc_vars.yml
```
This vars_files should be formated as:
```
ntp_servers:
  - name: 0.us.pool.ntp.org
timezone: 'UTC'
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
   - vars/chronyc_vars.yml
  roles:
  - proxmox-chronyc
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan