system-expand-disks
=========

Created to allow someone to resize disks. However, this was intended for use post-Terraform provisioning with a specific disk format. Please modify to fit your needs.

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- It also assumes that there is no firewall that may block connectivity, either on the NAS, network, or host.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
N/A

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure Disks Post Terraform
  hosts: new-host 
  become: true
  roles:
  - system-expand-disks
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan