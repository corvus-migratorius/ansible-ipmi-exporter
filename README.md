genlab.ipmi_exporter
=========

This Ansible role installs ipmi_exporter on target host. This is a Prometheus exporter for IP Management Interface metrics 

Requirements
------------

By default, the exporter relies on tools from the FreeIPMI suite for the actual IPMI implementation.

Role Variables
--------------
Configuration file must have names **ipmi_local.conf** and **web_conf.yaml** respectively.

```yaml
ipmi_exp_version: 1.10.1
ipmi_exp_dir: "/etc/exporters"
ipmi_exp_config_dir: "/etc/exporters/config"
ipmi_exp_log_level: "info"
ipmi_exp_log_format: "logfmt"
ipmi_exp_web_listen_address: "0.0.0.0:9290"
ipmi_exp_source_dir: ipmi_local.conf #     --config.file=CONFIG.FILE  Path to configuration file.
ipmi_exp_web_source_dir: web_conf.yaml # Path to configuration file that can enable TLS or authentication. See: https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md
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
      ipmi_exp_source_dir: "molecule/default/"
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
