genlab.ipmi_exporter
=========

This Ansible role installs ipmi_exporter on target host. This is a Prometheus exporter for IP Management Interface metrics 

Requirements
------------

By default, the exporter relies on tools from the FreeIPMI suite for the actual IPMI implementation.

Role Variables
--------------

```yaml
ipmi_exp_version: "1.10.1"
ipmi_exp_dir: "/etc/exporters"
ipmi_exp_config_dir: "/etc/exporters/config"
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
  roles:
    - role: genlab.ipmi_exporter
      ipmi_exp_version: "1.10.1"
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
