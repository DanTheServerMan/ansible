system-users
=========

Created to automate the configuration of local user accounts on Linux. It allows basic configuration of:
- Username
- Password
- Additional groups
- Decide if you will make a home or not
- Sudo access

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on other versions.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:
```
users:
- username: ansible
  password: '{{ user_password }}'
  create_home: true
  group: docker 
  shell: /bin/bash
  sudo: true
  sudo_config: 'ALL=(ALL:ALL) NOPASSWD:ALL'
  state: present
- username: ansible1
  password: '{{ user_password }}'
  create_home: true
  group: docker 
  shell: /bin/bash
  sudo: false
  sudo_config: 'ALL=(ALL:ALL) ALL'
  state: present
- username: ansible2
  password: '{{ user_password }}'
  create_home: true
  group: docker 
  shell: /bin/bash 
  sudo: false
  sudo_config: ''
  state: present
```
For ```user_password```, I use ansible-vault to securely store the credential.

If you don't want the user to be sudo, then just set ```sudo``` to false, and you can also remove the ```sudo_config``` line. The same can be said for any other field, if you don't want to create a home, remove ```create_home``` from your array, and then ```create_home``` from the tasks/main.yml play. 

If ```sudo: true``` AND ```state: present```, it will trigger the task to configure sudo access. It will use a Jinja template to configure ```/etc/sudoers.d/``` based on a combo of ```username sudo_config``` in that file.

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure local users
  hosts: homelab 
  vars_files:
   - vault/vault
  become: true
  roles:
  - system-users
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan