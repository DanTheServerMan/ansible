system-server-nfs
=========

Created to automate the creation of NFS servers and their exports. It installs nfs-kernel-server, starts it, enables it, creates your exported directory (if not created), and then exports it. This can be followed up with my system-mount-nfs role to configure the NFS clients to mount this export.

Requirements
------------

- A Linux machine with network connectivity to both your device and the internet for package downloads.
- It also assumes that there is no firewall that may block connectivity, either on the NAS, network, or host.
- This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
This playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:

```
# Items in /etc/exports
nfs_config:
  - export_host: 192.168.1.107
    export_dir: /test
    export_opt: (rw,sync,no_subtree_check)
```

You can add in multiple servers to that file, using the example above, and it will loop through the array, adding multiple lines to /etc/exports. 

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure NFS server exports
  hosts: nfs-servers 
  become: true
  roles:
  - system-server-nfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan