Ansible Role: Passenger
=========

Installs and configures Phusion Passenger as an application server

WIP Notice
----------

This role is a Work-In-Progress. It is limited in the following ways:

* Simply installs and does just enough configuration to be useful
* Only integrates with Apache, not with Nginx or stand-alone
* Only the open-source version is supported (not enterprise)
* Currently, only CentOS7 is supported

Requirements
------------

Apache HTTP Server. Nginx could also be used, but it is not currently supported by this role.

Role Variables
--------------

TBD

Dependencies
------------

A role, such as [this one](https://github.com/dheles/ansible-role-apache), that installs Apache HTTP Server. Nginx could also be used, but it is not currently supported by this role.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: passenger }

License
-------

CC0

Author Information
------------------

Drew Heles
