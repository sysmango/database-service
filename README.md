Database-Service
=========

An Ansible role to install database services in my home docker swarm.

Requirements
------------

This role assumes [HashiCorp Vault][1] is being utilized to manage secrets.
In order to use this role, ansible-modules-hashivault must be installed.

```
pip install ansible-modules-hashivault
```

Role Variables
--------------

postgres-password: Password for the postgresql service account that owns the database instance.  

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------


    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

