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

Note that the template, `default_passenger_virtualhost.j2` contains a variable `chruby_ruby_version` that must be set in advance. In our use of this role, the `chruby_ruby_version` variable is set by the `ansible-role-chruby` role which must be run prior.

Role Variables
--------------

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
