docker-nginx-fileserver
=========

Created to automate the deployment of a nginx file server via Docker. This can be helpful if you wish to view a specific folder in you web browser, or fetch files from a Linux box via http. In my case, its helpful for my homelab and ISO files. 

An example nginx.conf does exist in templates/ that serves the purpose of the file server, accessible via host:8080

The default directory exposed via the webserver has a root directory of /docker/nginx/files/. The root directory of /docker/ can be changed via the ```docker_container_data_directory``` variable. 

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the base directory for the docker containers. You can provide these variables either as a vars_files, in the playbook, or using group_vars:

```
docker_container_data_directory: /docker
```

It will be used by the vars.yml file as follows:
```
directories:
  - name: ISOs
  - name: Files

nginx:
  - name: nginx
    image: nginx:latest
    state: started
    volume:
    - '{{ docker_container_data_directory }}/nginx-ansible/files:/usr/share/nginx/html:ro'
    - '{{ docker_container_data_directory }}/nginx/nginx.conf:/etc/nginx/nginx.conf:ro'
    recreate: true
    published_ports:
      - "8080:80"
```


The variable configuration will configure the following directory structure. 

```
nginx-ansible/
├── files
│   ├── Files
│   └── ISOs
└── nginx.conf
```

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure nginx fileserver
  hosts: nginx 
  become: true
  roles:
  - docker-nginx-fileserver
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan