genlab.ipmi_exporter
=========

This Ansible role installs `ipmi_exporter` on target host - a Prometheus exporter for IPMI (Intelligent Platform Management Interface). See [metrics](https://github.com/prometheus-community/ipmi_exporter/blob/master/docs/metrics.md).

Requirements
------------

The exporter relies on tools from the FreeIPMI suite for the metrics it scrapes. OpenIPMI is not a valid replacement (the exporter won't find any collectors).

Collectors
----------

`ipmi_up{collector="<NAME>"}` is `1` if the data for this collector could successfully be retrieved from the remote host, `0` otherwise. The following collectors are available and can be enabled or disabled in the config:

- `ipmi`: collects IPMI sensor data.
- `dcmi`: collects DCMI data, currently only power consumption.
- `bmc`: collects BMC details.
- `bmc-watchdog`: collects status of the watchdog.
- `chassis`: collects the current chassis power state (on/off).
- `sel`: collects system event log (SEL) details.
- `sel-events`: collects metrics for user-defined events in system event log (SEL).
- `sm-lan-mode`: collects the "LAN mode" setting in the current BMC config.

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

See `molecule/default/converge.yml`.

License
-------

BSD

Author Information
------------------

msayganov@gmail.com

corvus-migratorius@proton.me
