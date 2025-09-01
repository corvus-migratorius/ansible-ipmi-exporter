genlab.ipmi_exporter
=========

This Ansible role installs ipmi_exporter on target host. This is a Prometheus exporter for Intelligent Platform Management Interface [metrics](https://github.com/prometheus-community/ipmi_exporter/blob/master/docs/metrics.md)

Requirements
------------

By default, the exporter relies on tools from the FreeIPMI suite for the actual IPMI implementation.

Collectors
----------

`ipmi_up{collector="<NAME>"}` is `1` if the data for this collector could successfully be retrieved from the remote host, `0` otherwise. The following collectors are available and can be enabled or disabled in the config:

- `ipmi`: collects IPMI sensor data. If it fails, sensor metrics (see below) will not be available
- `dcmi`: collects DCMI data, currently only power consumption. If it fails, power consumption metrics (see below) will not be available
- `bmc`: collects BMC details. If it fails, BMC info metrics (see below) will not be available
- `bmc-watchdog`: collects status of the watchdog. If it fails, BMC watchdog metrics (see below) will not be available
- `chassis`: collects the current chassis power state (on/off). If it fails, the chassis power state metric (see below) will not be available
- `sel`: collects system event log (SEL) details. If it fails, SEL metrics (see below) will not be available
- `sel-events`: collects metrics for user-defined events in system event log (SEL). If it fails, SEL entries metrics (see below) will not be available
- `sm-lan-mode`: collects the "LAN mode" setting in the current BMC config. If it fails, the LAN mode metric (see below) will not be available

Role Variables
--------------

- `ipmi_exp_version`: 1.10.1
- `ipmi_exp_config_dir`: where to put configuration files
- `ipmi_exp_args`:
  - `--[no-]native-ipmi`: use native IPMI implementation instead of FreeIPMI (EXPERIMENTAL)
  - `--[no-]web.systemd-socket`: use systemd socket activation listeners instead of port listeners (Linux only).
- `ipmi_exp_log_level`: one of: `[debug, info, warn, error]`
- `ipmi_exp_log_format`: one of: `[logfmt, json]`
- `ipmi_exp_web_listen_address`: address on which to expose metrics and web interface; repeatable for multiple addresses
  - `:9100` or `[::1]:9100` for HTTP
  - `vsock://:9100` for vsock
- `ipmi_exp_local_conf_path`: path to local configuration file, see: https://github.com/prometheus-community/ipmi_exporter/blob/master/docs/configuration.md
- `ipmi_exp_web_conf_path`: path to Web configuration file that can enable TLS or authentication, see: https://github.com/prometheus/exporter-toolkit/blob/master/docs/web-configuration.md


Dependencies
------------

None

Example Playbook
----------------

```yaml
  roles:
    - role: genlab.ipmi_exporter
      ipmi_exp_version: "1.10.1"
      ipmi_exp_local_conf_path: "molecule/default/"
```

License
-------

BSD

Author Information
------------------

corvus-migratorius@proton.me
