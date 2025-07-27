system-install-mullvad
=========

Created to automate the installation and connection of Mullvad VPN. It will download the signing key, add the repo, install the package, sign into your account, and automatically login to a specified server. It also enables LAN access and ensures the VPN will reconnect on boot.

Requirements
------------

- A Linux machine with network connectivity to both your device.
- This role was developed targeting Ubuntu 22.04 and has not been tested on a Red Hat-based system.

Role Variables
--------------
 
This playbook requires you to define a valid Mullvad Account Number. It must have a slot open for a new device, and have a functioning subscription.

You must also specify a location. To find a list of locations, you can view them here: https://mullvad.net/en/servers . In my example, I specified Atlanta in the United States. It will auto find a server in Atlanta. You could specify a country, country + city, or specific servers. 
```
mullvad_account: 123456789
mullvad_location: us atl
```

Example Playbook
----------------

Here is an example playbook, using the role, with the assumption the variables are provided in some way (ex. group_vars):
```
- name: Install Mullvad VPN
  hosts: dockarr 
  become: true
  roles:
  - system-install-mullvad
```
License
-------

BSD

Author Information
------------------

Created by DanTheServerMan