flyway
=========

Installs flyway commandline tool from http://flywaydb.org/getstarted/download.html to /opt/flyway and creates symlink from /usr/bin/flyway.


Requirements
------------

Ansible 1.4+. You'll need java on the host to use flyway, but role will succeed even without java.

Role Variables
--------------
All variables are optional

fly_version: (default: "3.1")

flyway_download_url: (default: "http://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/%s/flyway-commandline-%s.tar.gz")

flyway_root: (default: /opt/flyway)


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: javadb
      roles:
         - { role: flyway }
      vars:
         - { flyway_root: /opt/flyway }

License
-------

BSD

Author Information
------------------

(c) George Shuklin, 2015
