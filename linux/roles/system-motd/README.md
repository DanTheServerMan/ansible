system-motd
=========

Created to automate the configuration of login banners in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device.

This role was developed targeting Ubuntu 22.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
No variables are defined in the role or playbook.

However, if you want to change the banner, modify the Jinja template in templates/

Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ALL
  hosts: docker 
  become: true
  roles:
  - system-motd
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan