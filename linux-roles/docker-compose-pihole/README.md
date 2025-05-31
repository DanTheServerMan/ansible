docker-compose-pihole
=========

Created to automate the deployment of PiHole via Docker in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the following variables. You can provide these variables either as a vars_files, in the playbook, or using group_vars:
```
docker_container_directory: /docker/
docker_compose_directory: /docker/compose
```

You also need to define the variable 'password' in some way. How you do that is up to you. Ultimately, the password is in plain-text in the compose-file.

You could use a vault ('ansible-vault create pihole_password_vault')
```
  vars_files:
    - pihole_password_vault 
```
Or you could change 'vars:' to this:
```
  vars:
    password: testing123
```

Dependencies
------------

No dependencies, the only external data used was the compose file. I grabbed it (and the link is in the .j2 file) from here: https://github.com/pi-hole/docker-pi-hole/ . It is the same file, just used as a Jinja template, allowing us to put variables in.

Example Playbook
----------------

Here is an example playbook, using the role, specifying the vault file, with the assumption the remaining variables are provided in some way (ex. group_vars):
```
- name: Deploying pihole
  hosts: pihole 
  become: true
  vars_files:
    - pihole_password_vault 
  roles:
  - docker-compose-pihole
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan