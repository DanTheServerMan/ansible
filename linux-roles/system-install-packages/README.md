system-install-packages
=========

Created to automate the installation of multiple packages on Linux.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
```
packages:
  - docker.io
```

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Install packages
  hosts: homelab 
  become: true
  roles:
  - system-install-packages
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan