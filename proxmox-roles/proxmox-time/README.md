proxmox-time
=========

Created to automate the configuration of time on ProxMox.

I noticed, perhaps ancedotally on 9.0.6, that setting the timezone for the OS did not reflect the timezone available in the UI (under Host > System > Time) - I have since added an API call to set it via the API *in addition* to the host OS.

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

Besides the password, this playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
```
ntp_servers:
  - name: 0.us.pool.ntp.org
timezone: 'UTC'
```
Note that iburst is defined statically in the Jinja template. If you don't want it, you can modify the template.


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
  - proxmox-time
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan