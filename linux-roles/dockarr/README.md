dockarr
=========

Created to automate the deployment of my Linux ISOs downloads via Docker in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------

Variables were split between the vars file and playbook to allow easy tweaking of things I think you're more likely to change or tweak (like disabling a install, base docker directory, etc.)

The following vars in the playbook are required:
```
  vars:
    dockarr_container_config_directory: /dockarr/
    dockarr_container_data_directory: /nfs/
```

Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: Deploying Dockarr Homelab
  hosts: dockarr 
  become: true
  vars:
    dockarr_container_config_directory: /dockarr/
    dockarr_container_data_directory: /nfs/
  roles:
  - dockarr
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan