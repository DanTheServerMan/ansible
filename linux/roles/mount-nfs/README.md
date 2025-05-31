docker-nginx
=========

Created to automate the configuration of NFS datastores in my homelab.

Requirements
------------

A Linux machine with network connectivity to both your device, the internet for package downloads, and a functioning NFS export. 

Role Variables
--------------
 
The following vars in the playbook are required:
```
  vars:
    nfs_server: 192.168.1.10
    nfs_mount: /volume1/NFS
    nfs_opts: rw,sync,nfsvers=3
    nfs_state: mounted
    mount_point: /docker/
```

Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ALL
  hosts: docker 
  become: true
  vars:
    nfs_server: 192.168.1.10
    nfs_mount: /volume1/NFS
    nfs_opts: rw,sync,nfsvers=3
    nfs_state: mounted
    mount_point: /docker/
  roles:
  - mount-nfs 
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan