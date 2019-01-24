Role Name
=========

playbook for install sentry 8.22.0 and 9.0.0

Requirements
------------

- Postgresql
- Redis

Role Variables
--------------

```yml
sentry_search_config_path:  "{{ playbook_dir }}/files/groups/{{ item }}/sentry"

sentry_host_redis_config_file_path: "{{ sentry_host_redis_config_path | default(inventory_hostname) }}/config.yml.j2"
sentry_host_postgres_config_file_path: "{{ sentry_host_postgres_config_path | default(inventory_hostname) }}/sentry.conf.py.j2"

sentry_redis_config_file_path: /etc/sentry/config.yml
sentry_postgres_config_file_path: /etc/sentry/sentry.conf.py
sentry_config_path: /etc/sentry

sentry_system_user: that user for run sentry
sentry_version: support 2 verion (8.22.0, 9.0.0)

sentry_virtualenv_path: path for store virtualenv of sentry
sentry_system_secret_key: use for sentry system.secret
sentry_virtualevn_python_version: python2.7

sentry_admin: superuser for login sentry web

this example of configure file on files directory
variable use in template of config
 sentry_configuration:
   db_host: sentry.db.postgres
   db_host: 127.0.0.1
   db_port: 5432
   db_user: sentry
   db_password: CHANGEME
   db_name: sentry
   redis_host: 127.0.0.1
   redis_port: 6379
```

Dependencies
------------

Example Playbook
----------------

```yml
- hosts: all
  gather_facts: yes
  become: true
  roles:
    - { role: opsta.redis, when: sentry_all_in_one | default(false) }
    - { role: opsta.postgresql, when: sentry_all_in_one | default(false) }
    - opsta.sentry
```

License
-------

MIT

Author Information
------------------

Opsta Thailand
