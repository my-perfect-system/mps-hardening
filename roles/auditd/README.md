---
namespace: mps
collection: hardening
role: auditd
---

# `mps.hardening.auditd`

Install auditd apt package and write config + systemd override

## Default variables

| Variable | Default | Description |
|---|---|---|
| `auditd_admin_space_left` | `50` | Admin space left percentage threshold |
| `auditd_admin_space_left_action` | `SUSPEND` | Action when admin_space_left reached |
| `auditd_config_path` | `/etc/audit/auditd.conf` | Path to the auditd config file |
| `auditd_disk_error_action` | `SUSPEND` | Action on disk error |
| `auditd_disk_full_action` | `SUSPEND` | Action when disk full |
| `auditd_flush` | `INCREMENTAL` | Flush mode (NONE, INCREMENTAL, DATA, SYNC) |
| `auditd_freq` | `50` | Flush frequency (when flush=INCREMENTAL/DATA/SYNC) |
| `auditd_localstatedir` | `/var` | Override localstatedir in the auditd systemd unit (matches source) |
| `auditd_log_file` | `/var/log/audit/audit.log` | Path to the audit log file |
| `auditd_log_format` | `RAW` | Log format (RAW or ENRICHED) |
| `auditd_max_log_file` | `8` | Max log file size in MB before rotation |
| `auditd_max_log_file_action` | `ROTATE` | Action when max_log_file reached |
| `auditd_override_dir` | `/usr/lib/systemd/system/auditd.service.d` | systemd drop-in directory for auditd.service |
| `auditd_override_path` | `{{ auditd_override_dir }}/override.conf` | Path to the auditd systemd drop-in file |
| `auditd_packages` | `- auditd` | Apt packages required for auditd |
| `auditd_rules_dir` | `/etc/audit/rules.d` | Directory for audit rules |
| `auditd_run_dir` | `/var/run/audit` | Runtime directory for auditd |
| `auditd_space_left` | `75` | Free space left percentage warning threshold |
| `auditd_space_left_action` | `SYSLOG` | Action when space_left reached |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - mps.hardening.auditd
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: GPL-3.0-or-later
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 52

## Related files

- [`meta/main.yml`](meta/main.yml) — galaxy_info + role dependencies
- [`meta/argument_specs.yml`](meta/argument_specs.yml) — variable spec (the source of the variable table above)
- [`defaults/main.yml`](defaults/main.yml) — variable defaults (the source of the default values above)
