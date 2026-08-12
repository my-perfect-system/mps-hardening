---
# Reference doc — auto-generated, do not edit by hand.
# Regenerate via: python3 manage/gen_role_readmes.py
namespace: mps
collection: hardening
role: apparmor
---

# `mps.hardening.apparmor`

Install AppArmor profile packages and deploy profiles

## Default variables

| Variable | Default | Description |
|---|---|---|
| `apparmor_packages` | `- apparmor-utils<br>- apparmor-profiles<br>- apparmor-profiles-extra<br>- rsync` | Apt packages required for AppArmor profiles |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - mps.hardening.apparmor
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: GPL-3.0-or-later
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 25

## Related files

- [`meta/main.yml`](meta/main.yml) — galaxy_info + role dependencies
- [`meta/argument_specs.yml`](meta/argument_specs.yml) — variable spec (the source of the variable table above)
- [`defaults/main.yml`](defaults/main.yml) — variable defaults (the source of the default values above)
