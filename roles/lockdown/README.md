---
namespace: mps
collection: hardening
role: lockdown
---

# `mps.hardening.lockdown`

Run CIS lockdown benchmarks

## Default variables

| Variable | Default | Description |
|---|---|---|
| `lockdown_cis_repo` | `https://github.com/ansible-lockdown/DEBIAN13-CIS` | Git URL for the DEBIAN13-CIS lockdown role |
| `lockdown_cis_version` | `main` | Git ref for the CIS role |
| `lockdown_enable_execute` | `false` | Actually execute the CIS site.yml playbook |
| `lockdown_firewall_package` | `iptables` | Firewall package for CIS (ufw, nftables, or iptables) |
| `lockdown_repos_dir` | `{{ lockdown_user_home }}/repo/github` | Base directory for cloned repositories |
| `lockdown_user` | `{{ ansible_user }}` | System user to clone repos under and execute the CIS playbook as |
| `lockdown_user_home` | `/home/{{ lockdown_user }}` | Home directory of the lockdown user |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - mps.hardening.lockdown
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: GPL-3.0-or-later
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 147

## Related files

- [`meta/main.yml`](meta/main.yml) — galaxy_info + role dependencies
- [`meta/argument_specs.yml`](meta/argument_specs.yml) — variable spec (the source of the variable table above)
- [`defaults/main.yml`](defaults/main.yml) — variable defaults (the source of the default values above)
