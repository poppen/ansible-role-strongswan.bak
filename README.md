# Ansible Role: strongSwan

[![CI](https://github.com/poppen/ansible-role-strongswan/actions/workflows/ci.yml/badge.svg)](https://github.com/poppen/ansible-role-strongswan/actions/workflows/ci.yml)

An ansible role that installs and enables strongswan on Linux.

This role uses a swanctl.conf instead of ipsec.conf, and uses distributions' packages only. (it means this role doesn't build and install strongswan from the source.)

most of the ideas are taken from https://github.com/serverbee/ansible-role-strongswan.

Tested on:

- Ubuntu 20.04 and 22.04
- Debian 11

## Requirements

None.

## Role Variables

### Required

- `strongswan_swanctl_settings`: Set all settings for swanctl.conf in YAML.

### Optional

- `strongswan_config_file`: stronswan configuration file. (Default: `/etc/strongswan.d/01-strongswan.conf`)
- `strongswan_swanctl_config_file`: swanctl configuration file. (Default: `/etc/swanctl/conf.d/swanctl.conf`)
- `strongswan_settings`: Set all settings for the strongswan configuration file in YAML. The default variable is the following:

  ```yaml
  strongswan_settings:
    charon:
      filelog:
        charon:
          path: &strongswan_log_path "/var/log/charon.log"
        stderr:
          ike: 2
          knl: 3
  ```

- `strongswan_log_rotation`: Set settings in Dict format for rotating the strongswan log. It includes the below keys:
    - `enable`: enabling the rotation. (Default `true`)
    - `conf_path`: the installing file path of the logrotate configuration file. (Default: `/etc/logrotate.d/charon`)
    - `log_path`: the file path of the log file. (Default: `*stronswan_log_path`. It indicates `/var/log/charon.log` in default setting)
    - `settings`: the settings of log rotation. The default content is the following:

      ```yaml
      missingok
      copytruncate
      compress
      notifempty
      daily
      rotate 5
      ```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - poppen.strongswan
```

## License

BSD-3-Clause

## Author Information

Shinsuke MATSUI
