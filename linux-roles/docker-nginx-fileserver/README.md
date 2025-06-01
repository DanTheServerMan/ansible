docker-nginx-fileserver
=========

Created to automate the deployment of a nginx file server via Docker. This can be helpful if you wish to view a specific folder in you web browser, or fetch files from a Linux box via http. In my case, its helpful for my homelab and ISO files. 

An example nginx.conf does exist in templates/ that serves the purpose of the file server, accessible via host:8080

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the base directory for the docker containers, and for the fileserver. You can provide these variables either as a vars_files, in the playbook, or using group_vars.

```
docker_container_config_directory: /container_config/
docker_container_data_directory: /nfs-containers/
```
The ```docker_container_config_directory``` is where the persistent state of the container will be stored, such as the nginx.conf file. The ```docker_container_data_directory``` is what the webUI will show as a fileserver as the base directory.

These will be the subdirectories made under ```docker_container_data_directory/your_containers_name/```, and what your nginx webUI will show. It is an array so you can add as many directories as you'd like.
```
nginx_fileserver_directories:
  - name: ISOs
  - name: Files
```

The variable configuration shown above will configure the following directory structure, with nginx-ansible beinbg the name of the container created in the directory path:

This in your ```docker_container_config_directory```
```
/container_config/
├── nginx-ansible
│   └── nginx.conf
```
This in your ```docker_container_data_directory```
```
/nfs-containers/
├── nginx-ansible
│   ├── Files
│   ├── ISOs
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