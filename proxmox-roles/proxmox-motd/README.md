proxmox-motd
=========

Created to automate the configuration of a login banner on ProxMox that can be seen when connecting with SSH, or the console

Requirements
------------

- A ProxMox installation with network connectivity to your device.
- This role was developed targeting PVE 9.0.6.

Role Variables
--------------
 
No variables are defined in the role or playbook.

If you wish to modify the login banner, modify the Jinja template in templates/

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