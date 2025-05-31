Role Name
=========

Created to automate the deployment of a nginx file server via Docker in my homelab.

An example nginx.conf does exist in templates/ that serves the purpose of the file server, accessible via host:8080 

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

Role Variables
--------------
 
The variable configuration will configure the following directory structure. You can change the variables below to fit your use case.

Variables were split between the vars file and playbook to allow easy tweaking of things I think you're more likely to change or tweak (like disabling a install, base docker directory, etc.)

```
/docker/
├── nginx
│   ├── files
│   └── nginx.conf
```

The following vars in the playbook are required:
```
  vars:
    docker_compose_directory: /docker/compose
    install_pihole: 'true'
  vars_files:
    - vars/pihole_password_vault # Script expects variable name of 'password', NOTE that the password will be plain text in the compose file. You can just remove vars_files and add a vars: password: if you wish.
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
    install_nginx: 'true'
  vars_files:
    - vars/docker-vars.yml
  roles:
  - deploy-nginx
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan