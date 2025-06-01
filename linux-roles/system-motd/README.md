system-motd
=========

Created to automate the configuration of login banners on Linux.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
No variables are defined in the role or playbook. It will automatically use Ansible to identify and input the hostname and IP address into the motd.

However, if you want to change the banner itself, modify the Jinja template in templates/

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure motd
  hosts: homelab 
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