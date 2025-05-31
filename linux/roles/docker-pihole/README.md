docker-pihole
=========

Created to automate the deployment of PiHole via Docker in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

Role Variables
--------------
 
The variable configuration will configure the following directory structure. You can change the variables below to fit your use case.

```
docker/
├── compose
│   └── pihole
│       └── docker-compose.yml
```
Variables were split between the vars file and playbook to allow easy tweaking of things I think you're more likely to change or tweak (like disabling a install, base docker directory, etc.)

The following vars in the playbook are required:
```
  vars:
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
    docker_compose_directory: /docker/compose
    password: testing123
```

And the following vars/docker-vars.yml is required. You can also hard code it in the pihole-compose.yml.j2 if you'd prefer not to have a vars file.

```
version: latest
timezone: UTC
```
Dependencies
------------

No dependencies, the only external data used was the compose file. I grabbed it (and the link is in the .j2 file) from here: https://github.com/pi-hole/docker-pi-hole/ . It is the same file, just used as a Jinja template, allowing us to put variables in.

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: Deploying Docker Homelab
  hosts: docker 
  become: true
  vars:
    docker_container_directory: /docker/
    docker_compose_directory: /docker/compose
  vars_files:
    - vars/pihole_password_vault 
  roles:
  - docker-nginx
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan