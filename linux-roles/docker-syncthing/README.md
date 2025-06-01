docker-syncthing
=========

Created to automate the deployment of SyncThing via Docker. SyncThing is a fantastic tool to keep directories on different servers/hosts in sync. It will automatically pull the latest container image and start the container.

It is intended for a single SyncThing folder, but you can easily modify vars/main.yml and the variables to support multiple.

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the base directory for the docker containers, and your SyncThing directory/repos. You can provide these variables either as a vars_files, in the playbook, or using group_vars:

```
docker_container_data_directory: /nfs-containers/
syncthing_directory: /nginx-ansible/
syncthing_repo: /nginx
```
```docker_container_data_directory``` is the persistent storage configuration and where your containers configuration file will be stored.

```syncthing_directory``` is the underlying host volume that is passed through to the container, and in this case, intended to be sync'd. It needs to be the full path.

In the UI, ```syncthing_repo``` is what path you'll put as the folder path. So, with the above, you'd put ```/nginx``` in Folder Path. It is the containers perspective of ```syncthing_directory```.

The variable configuration will configure the following directory structure. 
 
```
/nfs-containers/
└── nginx-ansible
```

Please note I have added a second volume for a second repo to the main.yml file, you can either define the variables or remove that line.

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