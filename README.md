enix.timescaledb
=================

A role for deploying and configuring [timescaledb](http://timescale.com) and extensions on unix hosts using [Ansible](http://www.ansible.com/).


Requirements
------------

Supported targets:

- Ubuntu 20.04 "Focal"
- Ubuntu 22.04 "Jammy"
- Debian 10 "Buster"
- Debian 11 "Bullseye"


Role Variables
--------------

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in `defaults/main.yml` for help in configuration. All provided variables start with `timescaledb__`.

- `timescaledb__` - desc

Dependencies
------------

- [enix.postgresql](https://galaxy.ansible.com/enix/postgresql)


Usage
-----

Use Ansible galaxy requirements.yml

```
    # timescaledb from enix
    - src: enix.timescaledb
```

And add it to your play's roles:

```
    - hosts: all
      roles:
        - role enix.timescaledb:
            timescaledb__var: true
```

Still to do
-----------

- Write the role itself, for one


Changelog
---------

### 0.1

Initial version.

License
-------

GPLv2

Author Information
------------------

Laurent Corbes <laurent.corbes@enix.fr> - http://www.enix.io
