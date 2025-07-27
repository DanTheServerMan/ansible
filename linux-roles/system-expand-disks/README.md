system-expand-disks
=========

Created to automate the expansion of disk partitions and LVM after a VM is given more storage space. My use case is for expanding Packer template VMs with Terraform

NOTE: Some people might disagree with my method, but I don't feel like mounting a live ISO to properly repartition disks. Use at your own risk.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on other versions.

Role Variables
--------------
 
Right now, all values are static in the role itself. This will be updated later.

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Post-Terraform Disk Expansion
  hosts: new-terraform-hosts
  become: true
  roles:
  - system-expand-disks
  tags:
  -  new-terraform-hosts
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan