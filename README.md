Role Name
=========

Installs graylog role https://www.graylog.org/

[![Build Status](https://travis-ci.org/mrlesmithjr/ansible-graylog.svg?branch=master)](https://travis-ci.org/mrlesmithjr/ansible-graylog)

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

````
enable_graylog_server: true
enable_graylog_web: true
es_cluster_name: graylog
es_replicas: 0 #set to the number of replicas to set for the elasticsearch cluster - this applies to graylog server settings and elasticsearch
es_shards: 4 #set to the number of shards to set for the elasticsearch cluster - this applies to graylog server settings and elasticsearch
graylog_package_url: https://packages.graylog2.org/repo/packages/graylog-1.1-repository-ubuntu14.04_latest.deb
graylog_server_master: true #default is true unless installing multiple instances
graylog_server_password_secret: ''  #define in group_vars/all/accounts or generate new pw using...pwgen -N 1 -s 96
graylog_server_rest_listen_uri: http://127.0.0.1:12900/
graylog_server_root_password: '' #define in group_vars/all/accounts or generate new pw using...echo -n yourpassword | shasum -a 256
graylog_server_syslog_input_port: 10514 #set to port to be defined in graylog inputs
graylog_server_syslog_input_protocol: udp #udp or tcp
graylog_web_application_secret: ''  #define in group_vars/all/accounts or generate new pw using...pwgen -N 1 -s 96
graylog_web_server_uri: '{{ graylog_server_rest_listen_uri }}' #set to same as graylog_server_rest_listen_uri unless not installing both server and web on same host
port_redirects:  #define ports to port forward from system to graylog_server - only required for ports below 1024
  - syslog_dport: 514
    graylog_dport: 10514
    prot: udp
````

Dependencies
------------

````
mrlesmithjr.snmpd
mrlesmithjr.timezone
mrlesmithjr.elasticsearch
mrlesmithjr.mongodb
````

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mrlesmithjr.snmpd }
         - { role: mrlesmithjr.timezone }
         - { role: mrlesmithjr.elasticsearch }
         - { role: mrlesmithjr.mongodb }
         - { role: mrlesmithjr.graylog }

License
-------

BSD

Author Information
------------------

Larry Smith Jr.
- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
