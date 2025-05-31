docker-nginx
=========

Created to automate the deployment of a nginx file server via Docker in my homelab.

An example nginx.conf does exist in templates/ that serves the purpose of the file server, accessible via host:8080

The default directory exposed via the webserver has a root directory of /docker/nginx/files/. The root directory of /docker/ can be tweaked via the docker_container_directory directory. 

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

Role Variables
--------------
 
The variable configuration will configure the following directory structure. You can change the variables below to fit your use case.

```
/docker/
├── nginx
│   ├── files
│   └── nginx.conf
```

Variables were split between the vars file and playbook to allow easy tweaking of things I think you're more likely to change or tweak (like disabling a install, base docker directory, etc.)

The following vars in the playbook are required:
```
  vars:
    docker_container_directory: /docker/
```

And the following vars/docker-vars.yml is required. The 'state' was set to 'started' to apply new nginx.conf configurations, but you can adjust as needed.

```
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

Here is an example playbook, using the role, with variables in place:
```
- name: Deploying Docker Homelab
  hosts: docker 
  become: true
  vars:
    docker_container_directory: /docker/
  vars_files:
    - vars/docker-vars.yml
  roles:
  - docker-nginx
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan