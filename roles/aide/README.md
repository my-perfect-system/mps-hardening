---
# Reference doc — auto-generated, do not edit by hand.
# Regenerate via: python3 manage/gen_role_readmes.py
namespace: mps
collection: hardening
role: aide
---

# `mps.hardening.aide`

Install AIDE and deploy an exclusions drop-in

## Default variables

| Variable | Default | Description |
|---|---|---|
| `aide_confd_dir` | `/etc/aide/aide.conf.d` | Directory holding AIDE drop-in configs |
| `aide_exclusions_file` | `70_exclusions.conf` | Filename of the rendered exclusions drop-in |
| `aide_exclusions_path` | `{{ aide_confd_dir }}/{{ aide_exclusions_file }}` | Full path of the rendered exclusions drop-in |
| `aide_packages` | `- aide<br>- aide-common` | Apt packages required for AIDE |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - mps.hardening.aide
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: G, P, L, -, 3, ., 0, -, o, r, -, l, a, t, e, r
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 25
