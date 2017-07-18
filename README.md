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
By default, this role will setup the box as an NTP client, using the host values you will setup in your playbook vars/group_vars folders.  For example, you might have an infratructure playbook called `hostconfig.yml` that pulls in the chront role:

```yaml
roles:
    - ansible-sshd
    - ansible-chrony
```
and then a file in your **group_vars** folder that is named the same as a group in your inventory file, e.g. **ntp_servers**.

playbook vars file: **group_vars/ntp_servers**
```yaml
chrony_server: true
chrony_ntp_servers:
  - "0.us.pool.ntp.org iburst minpoll 8"
  - "1.us.pool.ntp.org iburst minpoll 8"
  - "2.us.pool.ntp.org iburst minpoll 8"
  - "3.us.pool.ntp.org iburst minpoll 8"
chrony_server_allow_nets:
  - "192.168.3/24"
```
this role's Jinja2 template file:
```jinja2
{% if chrony_server == true %}
{% for allow_net in chrony_server_allow_nets %}
allow {{ allow_net }}
{% endfor %}
{% endif %}
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

## Author

Dave Heebner <dave@rockpenguin.com>

&copy; 2017, Rockpenguin Technology, LLC
