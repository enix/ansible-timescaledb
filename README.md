# enix.timescaledb

A role for deploying and configuring [timescaledb](http://timescale.com) and extensions on unix hosts using [Ansible](http://www.ansible.com/).

## Requirements

Supported targets:

- Ubuntu 20.04 "Focal"
- Ubuntu 22.04 "Jammy"
- Debian 10 "Buster"
- Debian 11 "Bullseye"

## Role Variables

This roles comes preloaded with almost every available default. You can override each one in your hosts/group vars, in your inventory, or in your play. See the annotated defaults in `defaults/main.yml` for help in configuration. All provided variables start with `timescaledb__`.

- `timescaledb__version` - TimescaleDB main version to install. Curently only support '2'.
- `timescaledb__autotune` - Run `timescaledb-tune` to automatically configure the extension. default: `true`.
- `timescaledb__databases` - state of databases to be installed on the server. only mandatory parameter is name:

```yaml
postgresql__databases:
  - {name: test,
    lc_collate: 'en_US.UTF-8',
    lc_ctype: 'en_US.UTF-8',
    encoding: 'UTF-8',
    template: 'template0',
    owner: postgres,
    extension: [timescaledb],
    state: 'present'
   }
```

## Dependencies

- [enix.postgresql](https://galaxy.ansible.com/enix/postgresql)

## Usage

Use Ansible galaxy requirements.yml

```yaml
    # timescaledb from enix
    - src: enix.timescaledb
```

And add it to your play's roles:

```yaml
    - hosts: all
      roles:
        - role enix.timescaledb:
          timescaledb__version: 2
          postgresql__version: 14
          postgresql__global_config_options:
            - option: listen_addresses
              value: '*'
          postgresql__hba_entries:
            - {type: local, database: all, user: postgres, auth_method: peer}
            - {type: local, database: all, user: all, auth_method: peer}
            - {type: host, database: all, user: all, address: '0.0.0.0/0', auth_method: md5}
          postgresql__users:
            - {name: "testuser", password: "testuser"}
          timescaledb__databases:
            - {name: "timescale", owner: "testuser", extension: ["timescaledb"]}

```

## Still to do

## Changelog

### 1.0.0

Installation of TimeScaleDB PostgreSQL extension.
Add support for db creation.
Autotune the instance.

## License

GPLv2

## Author Information

Laurent Corbes <laurent.corbes@enix.fr> - http://www.enix.io
