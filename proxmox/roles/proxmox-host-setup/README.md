proxmox-host-setup
=========

This is a role I created to do a basic, initial ProxMox configuration in my homelab. It will:
- Install specific packages that I prefer working with that are not in the base install
- Switch the host to a free repository mode
- Set NTP
- Set a custom motd
- Mount a NFS share 

Requirements
------------

Requires ProxMox to be installed and accessible on the network.

There a few things that may vary between installations, such as enabling NFS storage. The primary playbook allows you to quickly toggle on or off (ir)relevant sections.

Further configuration (ex. NFS server IP, NFS path, etc.) can be found in vars/main.yml

Role Variables
--------------

The following are togglable in the playbook, which allows you to enable or disable sections of the role:
- upgrade_proxmox: 'false'
- free_repo_mode: 'true'
- set_clock: 'true' 
- set_motd: 'true' 
- configure_nfs: 'true'

Set as 'true' or 'false', anything other than 'true' will skip the task. Don't forget the '' !

In vars/main.yml you can find the following sections of variables:

Install, upgrade packages and ProxMox
```
pre_reboot_delay: # Time it takes to reboot the host after initiating it
packages:
  - name: # Name of a package you want installed, Add more bullet points for more packages
    state: # Tweak if you want a specific version, latest, or just present
```
Repository configuration
```
pve_enterprise_repo: # Make sure you use the latest repo link
ceph_enterprise_repo: # Make sure you use the latest repo linke
pve_nosub_repo: # Make sure you use the latest repo link
ceph_nosub_repo: # Make sure you use the latest repo link
```
NTP & System Clock
``` 
timezone: 
ntp_servers:
  - name: # Name of server 1, add another bullet point for additional ones. Assumes iburst.
```
NFS Server
```
nfs_storage: # Name of the datastore that will be shown in the UI
nfs_path: # NFS export path on the NFS server
nfs_ip: # NFS server IP
nfs_content:  # Content available on the datastore, options are under the 'content' section: https://pve.proxmox.com/wiki/Storage
```

Dependencies
------------

No dependencies.

Example Playbook
----------------

Here is an example playbook:

    - name: Initial ProxMox Host Deployment
      hosts: proxmox
      become: true
      vars:  
        upgrade_proxmox: 'false'
        free_repo_mode: 'true'
        set_clock: 'true' 
        set_motd: 'true' 
        configure_nfs: 'true' 
      roles:
      - proxmox-host-setup

License
-------

BSD

Author Information
------------------

Created by DanTheServerMan
