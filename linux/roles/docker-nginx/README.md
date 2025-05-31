docker-nginx
=========

Created to automate the deployment of a nginx file server via Docker in my homelab.

An example nginx.conf does exist in templates/ that serves the purpose of the file server, accessible via host:8080

The default directory exposed via the webserver has a root directory of /docker/nginx/files/. The root directory of /docker/ can be tweaked via the docker_container_directory directory. 

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
The variable configuration will configure the following directory structure. 

```
/docker/
├── nginx
│   ├── files
│   └── nginx.conf
```

This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:

```
docker_container_directory: /docker
nginx:
  - name: nginx
    image: nginx:latest
    state: started
    volume:
    - '{{ docker_container_directory }}/nginx/files:/usr/share/nginx/html:ro'
    - '{{ docker_container_directory }}/nginx/nginx.conf:/etc/nginx/nginx.conf:ro'
    recreate: true
    published_ports:
      - "8080:80"
```

Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure nginx fileserver
  hosts: nginx 
  become: true
  roles:
  - docker-nginx
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan