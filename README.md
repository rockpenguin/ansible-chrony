ansible-chrony
=========

Installs and configures the chronyd service for NTP.  This is for both server and client configuration.

Requirements
------------

* A supported distribution:
  * CentOS 7
  * Debian 8 (Jessie)
  * Ubuntu 16 (Xenial)

Role Variables
--------------

A list of the more common variables. For the defaults, it is good to check the [default vars](defaults/main.yml)

Example from the CentOS_7.yml vars file:

```yaml
chrony_os_supported: true
chronyd_binary: /sbin/chronyd
chronyc_binary: /bin/chronyc
chrony_service: chronyd
chrony_packages:
  - chrony
chrony_config_file: /etc/chrony.conf
chrony_keys_file: /etc/chrony.keys
chrony_drift_file: /var/lib/chrony/drift
chrony_config_file_owner: root
chrony_config_file_group: root
chrony_config_file_mode: "0644"
```

Dependencies
------------

None

Example Playbook
----------------

Just simply include the role within your playbook. If you need to adjust any of the vars, you can simply include a vars/distribution.yml (e.g. vars/CentOS_7.yml) file within your playbook structure.

    - hosts: www1 www2
      roles:
         - { role: username.rolename}

License
-------

BSD
