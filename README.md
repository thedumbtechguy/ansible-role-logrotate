# Ansible Role: logrotate

An ansible role to install and configure logrotate.

## Requirements

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `logrotate_conf_dir`: location of additional logrotate configurations.
  - Default: `/etc/logrotate.d`

- `logrotate_conf_scripts`: list of scripts to configure rotations.
  - Default: `[]`

### Script Definition

Each script in the list should conform to the following definition.

- `name`: a unique name for this script. usually the name of the service. e.g. `nginx`
  - **Required**

- `path`: path to logfile. e.g `/var/log/nginx/*.log`.
  - **Required**

- `options`: logrotate options.
  - Default: `[]`

- `postrotate`: scripts to execute after the rotation.
  - Default: `[]`

- `state`: state of this item.
  - Default: `present`
  - Options:
    - `present`
    - `absent`

## Usage Example

```yaml
- hosts: all
  vars:
    logrotate_conf_scripts:
      - name: semaphore
        path: /var/log/semaphore/*.log
        options:
          - rotate 14
          - daily
          - compress
          - delaycompress
          - sharedscripts
          - missingok
        postrotate:
          - /usr/sbin/service semaphore restart
  roles:
    - thedumbtechguy.logrotate
```


## License

MIT / BSD

## Author Information

This role was created by [Stefan Froelich](https://thedumbtechguy.blogspot.com/).

## Credits

This role was built upon the original work of:

- [nickjj/ansible-fail2ban](https://github.com/nickjj/ansible-fail2ban)

