storage-server-nfs (Work In Progress)
=========

NOTE: This role is currently a work in progress as an interesting side project.

Created to automate the configuration of ZFS zpools on Linux.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
There is one default variable in defaults/ , and that is ```wipe_disk: false```. If you want to wipe the disks for ZFS config, you should explicitly define this variable to be 'true'.


Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure zfs
  hosts: pi 
  become: true
  roles:
  - system-zfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan