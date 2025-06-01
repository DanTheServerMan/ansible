docker-pihole
=========

Created to automate the deployment of a PiHole server via Docker in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

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
This playbook requires you to define the base directory for the docker containers. You can provide these variables either as a vars_files, in the playbook, or using group_vars:

```
docker_container_directory: /docker
```

It will be used by the vars.yml file as follows:
```
pihole:
  - name: pihole-ansible
    image: "pihole/pihole:latest"
    state: started
    recreate: true
    restart_policy: unless-stopped
    pull: yes
    published_ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80/tcp"
      - "443:443/tcp"
    volumes:
      - "{{ docker_container_data_directory }}/pihole:/etc/pihole"
    env:
      TZ: "UTC"
      FTLCONF_webserver_api_password: "{{ password }}"
      FTLCONF_dns_listeningMode: "all"
    capabilities:
      - NET_ADMIN
      - SYS_TIME
      - SYS_NICE
```

Dependencies
------------

No dependencies

Example Playbook
----------------

Note you'll need to define a vars_files for the vault, used as the password.

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure pihole container
  hosts: docker 
  vars_files:
   - vault/vault
  become: true
  roles:
  - docker-pihole
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan