system-ufw
=========

Created to automate the configuration of UFW firewalls in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device.

This role was developed targeting Ubuntu 22.04 and has not been tested on other versions.

Role Variables
--------------
 
No vars in the playbook are required, however you must specify a vars_files of vars/ufw-vars.yml. 

You can add in multiple servers to that file, using the example below, and it will loop through the array, managing multiple firewall rules.

The variables defined do not allow every UFW module variable to be changed, such as managing traffic based on its protocol (TCP/UDP). You could add a field in the variables file, and modify the task file if you'd like to have more control. 

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
Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ALL
  hosts: ufw-hosts 
  become: true
  vars_files:
    - vars/ufw-vars.yml
  roles:
  - system-ufw
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan