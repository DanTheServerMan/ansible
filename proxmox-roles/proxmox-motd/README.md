proxmox-motd
=========

Created to automate the configuration of a login banner on ProxMox in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device.

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
No variables are defined in the role or playbook.

If you wish to modify the login banner, modify the Jinja template in templates/

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
  roles:
  - proxmox-motd
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan