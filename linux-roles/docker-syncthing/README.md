docker-syncthing
=========

Created to automate the deployment of SyncThing via Docker in my homelab. SyncThing is a fantastic tool to keep directories on different servers/hosts in sync. 

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

This playbook requires you to define the base directory for the docker containers, and your SyncThing directory/repos. You can provide these variables either as a vars_files, in the playbook, or using group_vars:

```
docker_container_data_directory: /docker
syncthing_directory: /nginx-ansible/files
syncthing_repo: /nginx
```
docker_container_data_directory is the persistent storage configuration and where your containers configuration file will be stored.

syncthing_directory is the underlying host volume that is passed through to the container, and in this case, intended to be sync'd.

In the UI, syncthing_repo is what path you'll put as the folder path. So, with the above, you'd put /nginx in Folder Path. It is the containers perspective of syncthing_directory.

It will be used by the vars.yml file as follows:
```
syncthing:
  - name: syncthing-ansible
    image: lscr.io/linuxserver/syncthing:latest
    state: started
    pull: true
    volume:
    - '{{ docker_container_data_directory }}/syncthing:/config'
    - '{{ docker_container_data_directory }}{{ syncthing_directory }}:/{{ syncthing_repo }}'
    published_ports:
      - "8384:8384"
      - "22000:22000/tcp"
      - "22000:22000/udp"
      - "21027:21027/udp"
    env:
      PUID: "1000"
      PGID: "1000"
      TZ: "Etc/UTC"
```


The variable configuration will configure the following directory structure. 

```
nginx-ansible/
├── files
│   ├── Files
│   └── ISOs
└── nginx.conf
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
  - docker-nginx-fileserver
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan