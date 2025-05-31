system-mount-nfs
=========

Created to automate the configuration of NFS datastores in my homelab.

It will also attempt to detect your OS and install either nfs-utils or nfs-common to allow the mount.

Requirements
------------

A Linux machine with network connectivity to both your device, the internet for package downloads, and a functioning NFS export. You can use my role system-server-nfs to configure the NFS export/server if you need assistance.

It also assumes that there is no firewall that may block connectivity, either on the NAS, network, or host.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
No vars in the playbook are required, however you must specify a vars_files of vars/nfs-vars.yml. You can use group_vars or another method based on your needs.

You can add in multiple servers to that file, using the example below, and it will loop through the array, adding multiple mounts in one go.

```
nfs_servers:
 -  nfs_server: 192.168.1.100
    nfs_export: /volume1/NFS-ISO
    nfs_opts: rw,sync,nfsvers=3
    nfs_state: mounted
    mount_point: /ISO/
```
Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: Configure NFS client mounts
  hosts: nfs-clients
  become: true
  vars_files:
    - vars/nfs-vars.yml
  roles:
  - system-mount-nfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan