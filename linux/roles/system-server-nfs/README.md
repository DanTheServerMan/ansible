system-update
=========

Created to automate the update of linux in my homelab. This can be followed up with my system-mount-nfs role to configure the NFS clients.

Requirements
------------

A Linux machine with network connectivity to both your device and the internet for package downloads.

It also assumes that there is no firewall that may block connectivity, either on the NAS, network, or host.

This role was developed targeting Ubuntu 24.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
No vars in the playbook are required, however you must specify a vars_files of vars/nfs-server-vars.yml. You can use group_vars or another method based on your needs.

You can add in multiple servers to that file, using the example below, and it will loop through the array, adding multiple lines to /etc/exports.

```
# Items in /etc/exports
nfs_config:
  - export_host: 192.168.1.107
    export_dir: /test
    export_opt: (rw,sync,no_subtree_check)
```
Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ALL
  hosts: nfs-servers 
  become: true
  vars_files:
    - vars/nfs-server-vars.yml
  roles:
  - system-server-nfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan