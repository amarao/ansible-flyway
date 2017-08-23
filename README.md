flyway
=========

Installs and configures flyway commandline tool from http://flywaydb.org/getstarted/download.html. It installs files to /opt/flyway and creates symlink from /usr/bin/flyway to the binary in the /opt/flyway.


Requirements
------------

Ansible 1.4+. You'll need java on the host to use flyway, but role will succeed even without java.

Role Variables
--------------
All variables are optional

- fly\_version: (default: "4.2.0")
- flyway\_download\_url: (default: "http://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/%s/flyway-commandline-%s.tar.gz")
- flyway\_root: (default: /opt/flyway)
- flyway\_config: 
  - database:
    - dbms:  (Tested with postgress and oracle)
    - host: db hostname or IP
    - port: 5432
    - name: database name
    - user: username
    - password: password for username
  - schemas: schemas to manage
- flyway\_table: flyway table (default schema\_history)
- flyway\_locations: path to sql migrations (with 'filesystem:' prefix if needed, see examples)
- flyway\_symlink\_location: place for executable symlink (default: /usr/bin)

Dependencies
------------

None

Example Playbook (postgres)
---------------------------

    - hosts: javadb
      roles:
         - { role: flyway }
      vars:
         - flyway_root: /opt/flyway
         - flyway_config:
            database: 
              host: localhost
              port: 5432
              dbms: postgresql
              name: example
              user: postgres
              password: postgres
            schemas: public, myschema
         - flyway_locations: filesystem:/opt/migrations/
         
Configuration tested with Postgres 9.2.
        
Example Playbook (Oracle)
-------------------------


    - hosts: oracledb
      roles:
         - { role: flyway }
      vars:
        - flyway_driver: oracle.jdbc.OracleDriver
        - flyway_config:
           database:
           dbms: oracle
           host: localhost
           port: 1521
           name: XE
           user: APP
           password: appsecret
           schemas: APP
        - flyway_locations: filesystem:/opt/migrations/full,filesystem:/opt/migrations/demo

Configuration tested with Oracle XE 11.

Note: you need to copy the driver jar to flyway:

```
- name: Copy Oracle JDBC driver to machine Flyway folder
  copy: src=./lib/ojdbc6-11.1.0.7.0.jar dest=/opt/flyway/flyway-{{ flyway_version }}/drivers
  sudo: yes
```

License
-------

BSD

Author Information
------------------

(c) George Shuklin 2015-2016, rastaman 2015
