flyway
=========

Installs and configures flyway commandline tool from http://flywaydb.org/getstarted/download.html to /opt/flyway, ceates symlink to proper binary from /usr/bin/flyway.


Requirements
------------

Ansible 1.4+. You'll need java on the host to use flyway, but role will succeed even without java.

Role Variables
--------------
All variables are optional

- fly_version: (default: "3.1")
- flyway_download_url: (default: "http://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/%s/flyway-commandline-%s.tar.gz")
- flyway_root: (default: /opt/flyway)
- flyway_config: 
  - database:
    - dbms:  (I didn't test it with mysql or something else, except postgresql)
    - host: db hostname or IP
    - port: 5432
    - name: database name
    - user: username
    - password: password for username
  - schemas: schemas to manage
- flyway_table: flyway table (default schema_history)
- flyway_locations: path to sql migrations

Dependencies
------------

None

Example Playbook
----------------

    - hosts: javadb
      roles:
         - { role: flyway }
      vars:
         - flyway_root: /opt/flyway
         - flyway_config:
            database: 
              host: localhost
              port 5432
              dbms: postgesql
              name: example
              user: postgres
              password: postgres
            schemas: public, myschema
         - flyway_locations: /opt/migrations/
        
Example configuration for Oracle
--------------------------------

```
flyway_driver: oracle.jdbc.OracleDriver
flyway_config:
  database:
    dbms: oracle
    host: localhost
    port: 1521
    name: XE
    user: GUT
    password: mdp4gut
  schemas: GUT
flyway_locations: filesystem:/opt/migrations/full,filesystem:/opt/migrations/demo,filesystem:/opt/migrations/tomcat
```

License
-------

BSD

Author Information
------------------

(c) George Shuklin, 2015
