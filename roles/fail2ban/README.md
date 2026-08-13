---
namespace: odem
collection: hardening
role: fail2ban
---

# `odem.hardening.fail2ban`

Install fail2ban and deploy the default sshd jail for SSH brute-force protection.

## Default variables

| Variable | Default | Description |
|---|---|---|
| `fail2ban_enable_service` | `true` | Toggle to install and run fail2ban entirely |
| `fail2ban_packages` | `- fail2ban` | Apt packages required for fail2ban |
| `fail2ban_jail_dir` | `/etc/fail2ban` | Root directory for fail2ban configuration |
| `fail2ban_jail_local_path` | `{{ fail2ban_jail_dir }}/jail.local` | Path to the umbrella jail.local file |
| `fail2ban_jail_d_dir` | `{{ fail2ban_jail_dir }}/jail.d` | Directory for per-jail drop-in configs |
| `fail2ban_jail_sshd_path` | `{{ fail2ban_jail_d_dir }}/sshd.local` | Path to the sshd jail drop-in |
| `fail2ban_sshd_enabled` | `true` | Enable the sshd jail |
| `fail2ban_sshd_backend` | `systemd` | fail2ban backend for log monitoring |
| `fail2ban_sshd_port` | `ssh` | Port or service name for the sshd jail |
| `fail2ban_sshd_logpath` | `/var/log/auth.log` | Log path monitored by the sshd jail |
| `fail2ban_sshd_maxretry` | `5` | Max retries before ban |
| `fail2ban_sshd_findtime` | `600` | Detection window in seconds |
| `fail2ban_sshd_bantime` | `600` | Ban duration in seconds |
| `fail2ban_service_name` | `fail2ban` | systemd service name for fail2ban |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - odem.hardening.fail2ban
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: GPL-3.0-or-later
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 35

## Related files

- [`meta/main.yml`](meta/main.yml) — galaxy_info + role dependencies
- [`meta/argument_specs.yml`](meta/argument_specs.yml) — variable spec (the source of the variable table above)
- [`defaults/main.yml`](defaults/main.yml) — variable defaults (the source of the default values above)
