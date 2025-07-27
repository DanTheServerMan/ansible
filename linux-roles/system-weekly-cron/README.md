system-cron
=========

This role creates cronjobs on the target hosts that are scheduled to run on specific week days. It is expected to run every month. 

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on other versions.

Role Variables
--------------
 
The role currently supports the following configurable fields:
```
cronjobs:
- name: 'Auto upgrade, every Sunday at 7:00am UTC'
  minute: '0'
  hour: '7'
  weekday: '0'
  job: 'sudo apt update && sudo apt upgrade -y && sudo reboot'
```

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Configure cronjobs
  hosts: homelab
  roles:
  - system-cron
  tags:
  -  cron
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan