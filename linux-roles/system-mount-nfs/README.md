system-mount-nfs
=========

Created to automate the configuration of mounting NFS datastores. This could be used after my system-server-nfs to create the exports. It attempt to detect your OS and install either nfs-utils or nfs-common to allow the mount. After that, it will try and mount the export.

Requirements
------------

- A Linux machine with network connectivity to both your device, the internet for package downloads, and a functioning NFS export. You can use my role system-server-nfs to configure the NFS export/server if you need assistance.
- It also assumes that there is no firewall that may block connectivity, either on the NAS, network, or host. 
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:

```
nfs_servers:
 -  nfs_server: 192.168.1.100
    nfs_export: /volume1/NFS-ISO
    nfs_opts: rw,sync,nfsvers=3
    nfs_state: mounted
    mount_point: /ISO/
```

You can add in multiple servers to that file, using the example above, and it will loop through the array, mounting each one. 

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure NFS client mounts
  hosts: nfs-clients
  become: true
  roles:
  - system-mount-nfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan