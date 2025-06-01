system-ufw
=========

Created to automate the configuration of a basic UFW firewall rules on Ubuntu. It will also start and enable the service.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on other versions.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:

```
ufw_rules:
 -  comment: Allow SSH
    src_host: any
    dest_host: any
    port: '22'
    action: allow
 -  comment: Allow HTTPS
    src_host: any
    dest_host: any
    port: '443'
    action: allow
```

The variables defined do not allow every UFW module variable to be changed, such as managing traffic based on its protocol (TCP/UDP). You could add a field in the variables file, and modify the task file if you'd like to have more control. 

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure UFW
  hosts: ufw-hosts 
  become: true
  roles:
  - system-ufw
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan