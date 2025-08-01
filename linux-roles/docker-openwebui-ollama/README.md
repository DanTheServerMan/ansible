docker-openwebui-ollama
=========

Created to automate the deployment of a OpenWebUI server via Docker. It also is set to allow Ollama. It will automatically pull the latest container image and start the container. 

This role does NOT enable any GPU connectivity.

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

Example Playbook
----------------

Note you'll need to define a vars_files for the vault, used as the password.

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Deploy OpenWebUI w/ Ollama
  hosts: openwebui 
  become: true
  roles:
  - docker-openwebui-ollama
```
License 
-------

BSD

Author Information
------------------

Created by DanTheServerMan