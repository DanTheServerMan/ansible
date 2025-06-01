docker-pihole
=========

Created to automate the deployment of a PiHole server via Docker. It will automatically pull the latest container image and start the container. It also sets the password for the webUI.

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the base directory for the docker containers. You can provide these variables either as a vars_files, in the playbook, or using group_vars:

```
docker_container_config_directory: /container-config
```

You also need to define the variable 'password' in some way. How you do that is up to you. This will be the password you use to sign into the webUI.

You could use a vault ('ansible-vault create pihole_password_vault') to define the variable, then call the vault in the playbook:
```
  vars_files:
   - vault/vault
```

Or you could change 'vars:' on the playbook to this:
```
  vars:
    password: testing123
```

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