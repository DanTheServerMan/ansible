proxmox-nfs
=========

Created to automate the configuration of NFS storage on ProxMox in my homelab.

While you can use blockinfile to directly manage /etv/pve/storage.cfg, in my experience, this started to have issues when having multiple datastores. Plus, I wanted to see what using the API would look like. So, you will have to handle credentials to use this module. See below.

Requirements
------------

A ProxMox installation with network connectivity to your device. It also assumes that there is a NAS on your network with properly configured exports.

This role was developed targeting PVE 8.4.

Role Variables
--------------
 
You need to define two variables for logging in. I recommend and use ansible-vault. The variables you need to define is:
```
username: [YOUR_USER]@[DOMAIN]
password: "[YOUR PASSWORD]"
```
An example would be:
```
username: root@pam
password: "password"
```
In your playbook, you can specify the vault:
```
  vars_files:  
   - vars/pve-vault # Or your other file
```

Besides the password, this playbook requires you to define the configuration as an array. You can provide these variables either as a vars_files, or using group_vars:

```
nfs_servers:
  - nfs_storage: # Name of the datastore that will be shown in the UI
    nfs_path: # NFS export path on the NFS server
    nfs_ip: # NFS server IP
    nfs_content: # Content available on the datastore, options are under the 'content' section: https://pve.proxmox.com/wiki/Storage
```
Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, specifying the vault, and with the assumption the variables are provided in some way (ex. group_vars):
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  vars_files:  
   - vars/pve-vault # Or your other file
  roles:
  - proxmox-nfs
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan