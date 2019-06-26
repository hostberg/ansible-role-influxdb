# Ansible Role: InfluxDB

[![Build Status](https://travis-ci.org/hostberg/ansible-role-influxdb.svg?branch=master)](https://travis-ci.org/hostberg/ansible-role-influxdb)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/badge/ansible%20role-hostberg.influxdb-blue.svg)](https://galaxy.ansible.com/hostberg/influxdb/)

Requirements
------------

None

Role Variables
--------------

| Name                                       | Default                       | Type   | Description                                    |
| ------------------------------------------ | ----------------------------- | ------ | ---------------------------------------------- |
| `influxdb_databases`                | []                                | Array  | Databases                                      |
| `influxdb_users`                    | []                                | Array  | Users                                          |
| `influxdb_privileges`               | []                                | Array  | Privileges                                     |
| `influxdb_config`                   | []                                | Array  | Configuration                                  |
| `influxdb_config_file`              | '/etc/influxdb/influxdb.conf'     | String | Configuration file path                        |
| `influxdb_config_template`          | 'config/base.conf.j2'             | String | Configuration template path                    |
| `influxdb_yum_repo_template`          | 'etc/yum.repos.d/influxdb.repo.j2' | String | Yum template to use

Use a custom InfluxDB Yum repo template example:

* Put your template next to your playbook under `templates` folder
* Use a different path than the default one, because ansible , when using relative path, use the first template found and look under the role directory at first then the playbook directory
* The template expansion will be put under  `/etc/yum.repos.d/` , and will have as a name, the `basename` of the template path without the .j2

  Example:

  ```yaml
  influxdb_yum_repo_template: my_yum_repos/influxdb.repo.j2

  # [playbook_dir]/templates/my_yum_repos/influxdb.repo.j2
  # will be put under
  # /etc/yum.repos.d/influxdb.repo
  # on the remote host
  ```

### Configuration example

```yaml
############
# InfluxDB #
############

influxdb_databases:
  - my_db

influxdb_users:
  - database: my_db
    name:     my_user
    password: my_password

influxdb_privileges:
  - database: my_db
    user:     my_user
    grant:    ALL

influxdb_config:
  - reporting-disabled: true
  - udp:
    - enabled: true
    - bind-address: :8089
    - database: stats
    - batch-size: 5000
    - batch-timeout: 1s
    - batch-pending: 10
    - read-buffer: 0
```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: hostberg.influxdb }

License
-------

MIT

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
