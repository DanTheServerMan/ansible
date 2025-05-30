Role Name
=========

Created to automate the deployment of PiHole via Docker in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

Role Variables
--------------
 
The following vars are required:
```
  vars:
    compose_directory: /containers/compose/pihole/
    container_data_directory: /containers/data/pihole/
    container_name: piholetesting
    version: latest
    timezone: UTC
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
    compose_directory: /containers/compose/pihole/
    container_data_directory: /containers/data/pihole/
    container_name: piholetesting
    version: latest
    timezone: UTC
    password: testing123
```
Dependencies
------------

No dependencies, the only external data used was the compose file. I grabbed it (and the link is in the .j2 file) from here: https://github.com/pi-hole/docker-pi-hole/ . It is the same file, just used as a Jinja template, allowing us to put variables in.

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
    - name: Deploy PiHole as a Docker container 
      hosts: pihole 
      become: true
      vars:
        compose_directory: /containers/compose/pihole/
        container_data_directory: /containers/data/pihole/
        container_name: piholetesting
        version: latest
        timezone: UTC
      vars_files:
        - pihole_password_vault 
      roles:
      - deploy-pihole-docker
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan