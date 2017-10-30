Role Name
=========

Installs and configures MySQL or MariaDB or Percona server on Ubuntu servers.

Requirements
------------

This role requires Ansible 2.3

Install
-------

ansible-galaxy install plumelo.mysql

Role Variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

```yaml
# Installation type(mysql is installed from other source and only want to configure mysql-server)
mysql_installation_type: ""
# mysql_installation_type: 'configuration_only'

# Choose database from mysql, mariadb, percona
mysql_package: mysql

# If percona, is necesary to specify the ppa version(or what you want)
percona_version: '5.7'

# Mysql hosts
mysql_hosts:
  - "{{ ansible_hostname }}"
  - localhost
  - ...

# Mysql name(project name) for create mysql database and path if you want to import one.
mysql_databases:
  - name: test
  - path: /your_path_to_db.sql

# Mysql users for define user or users.(options for name, password, whether the user should exist, host and privileges)
mysql_users:
  - name: user
    password:
      - 12345
    privs:
      - '*.*:ALL'
    hosts:
      - localhost
    state:
      - present

  - name: user1
    privs:
      - user1.*:ALL
    hosts:
      - 127.0.0.1

# Configures mysql server "/etc/mysql/conf.d/server.cnf".(put here the configs you want)
mysql_config:
  mysqld:
    port: 3306
    socket: /var/run/mysqld/mysql.sock
  mysql:
    no_auto_rehash: ~
    max_allowed_packet: 16M
    prompt: '\u@\h [\d]> '
    default_character_set: utf8
  mysqldump:
    max_allowed_packet: 16M
  mysqld_safe:
    open_files_limit: 8192
    user: mysql
    log-error: <hostname>_error.log
```

Dependencies
------------

No special requirements.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      become: 'yes'
      roles:
         - role: plumelo.mysql

License
-------

BSD

Author Information
------------------

- plumelo.com
