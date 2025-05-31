proxmox-single-host-update
=========

Created to automatically update ProxMox to the latest release, using dist-upgrade, in my homelab.

Requirements
------------

A ProxMox installation with network connectivity to your device.

This role was developed targeting PVE 8.4.

The assumption is that VMs and LXCs can be shutdown, AND that a ProxMox-initiated shutdown is acceptable. In the future I'd like to make a 'proxmox-multi-host-update' to handle migrations.

Role Variables
--------------
 
No variables are defined in the role or playbook.

Dependencies
------------

No dependencies

Example Playbook
----------------

Here is an example playbook, using the role, with variables in place:
```
- name: ProxMox Host Configuration
  hosts: proxmox
  become: true
  roles:
  - proxmox-single-host-update
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan