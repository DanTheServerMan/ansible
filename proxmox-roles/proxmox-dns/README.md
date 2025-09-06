proxmox-dns
=========

Created to automate the configuration of two DNS servers and a search domain. 

Requirements
------------

- A ProxMox installation with network connectivity to your device. 
- This role was developed targeting PVE 9.0.6.

Role Variables
--------------
 
You need to define two variables for logging in to generate a token before using the API. I recommend, and use, ansible-vault. The variables you need to define is:
```
username: [YOUR_USER]@[DOMAIN]
password: "[YOUR PASSWORD]"
```
An example would be:
```
username: root@pam
password: "password"
```
In your playbook, you can specify the vault:
```
  vars_files:  
   - vars/pve-vault # Or your other file
```

Besides the password, this playbook requires you to define the DNS configuration. You can provide these variables either as a vars_files, or using group_vars:

```
dns_searchdomain: lab
dns1: 192.168.1.110
dns2: 192.168.1.111
```

Example Playbook
----------------

Here is an example playbook, using the role, specifying the vault, and with the assumption the variables are provided in some way (ex. group_vars):
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  vars_files:  
   - vars/pve-vault # Or your other file
  roles:
  - proxmox-dns
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan