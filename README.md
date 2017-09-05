Ansible Role: Passenger
=========

Installs and configures Phusion Passenger as an application server

NOTE: This role is limited in the following ways:

* Only integrates with Apache, not with Nginx or stand-alone
* Only the open-source version is supported (not enterprise)
* Currently, only CentOS7 is supported

Requirements
------------

Apache HTTP Server. Nginx could also be used, but it is not currently supported by this role.

Role Variables
--------------

I couldn't get ansible's yum modules to work with phusion's repo and eventually just used the command module. This flag is used to control the flow from what should work to what does. The hope is that the issue might someday be resolved and we can just do things the "right" way.

    ansible_likes_passenger_repo:     false

Other variables that require much less explanation:

    passenger_update_packages:        "{{ update_packages | default(false) }}"
    passenger_deploy_rails:           true
    passenger_app_name:               "{{ app_name | default('myapp') }}"
    passenger_app_user:               "{{ app_user | default(passenger_app_name) }}"
    passenger_base_deploy_dir:        "{{ base_deploy_dir | default('/opt') }}"
    passenger_deploy_dir:             "{{ passenger_base_deploy_dir }}/{{ passenger_app_name }}"
    passenger_hostname:               "{{ hostname | default('myapp') }}"
    passenger_app_environment:        "{{ rails_env | default('production') }}"
    passenger_debugging:              "{{ debugging | default(false) }}"
    # NOTE: to successfully override this template, you MUST use a template file with a different name. now you know...
    passenger_virtualhost_template:   "default_passenger_virtualhost.j2"
    apache_config_file:               "/etc/{{ apache_service }}/conf.d/01_{{ passenger_hostname }}.conf"

Dependencies
------------

A role, such as [this one](https://github.com/dheles/ansible-role-apache), that installs Apache HTTP Server. Nginx could also be used, but it is not currently supported by this role.

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: apache }
         - { role: passenger }

License
-------

CC0

Author Information
------------------

Drew Heles
