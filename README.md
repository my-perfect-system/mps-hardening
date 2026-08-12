# `mps.hardening` Ansible Collection

System-level security hardening — firewall (iptables), apparmor
profiles, auditd, AIDE intrusion detection, CIS lockdown (clones
`ansible-lockdown/DEBIAN13-CIS`).

## Galaxy metadata

- **namespace**: `mps`
- **name**: `hardening`
- **version**: `0.3.1`
- **dependencies**: `mps.base`, `ansible.posix`, `community.crypto`

See [`galaxy.yml`](galaxy.yml) for the canonical values.

## Roles

| Role | Purpose |
|---|---|
| `mps.hardening.firewall` | iptables rules (templated with port ranges, ICMP, NAT). |
| `mps.hardening.apparmor` | Apparmor profile sync + enforce. |
| `mps.hardening.auditd` | auditd + auditd.conf + systemd override. |
| `mps.hardening.aide` | AIDE intrusion detection. |
| `mps.hardening.lockdown` | DEBIAN13-CIS clone + sub-playbook invocation (gated by `lockdown_enable_execute`). |

## Installation

```bash
ansible-galaxy collection install mps.hardening
ansible-galaxy collection install community.crypto
```

## Usage

```yaml
- hosts: all
  become: true
  roles:
    - mps.hardening.firewall
    - mps.hardening.apparmor
    - mps.hardening.auditd
    - mps.hardening.aide
    - mps.hardening.lockdown
```

## Caveats

- `firewall` and `lockdown` complexity is load-bearing — the templates and external-repo orchestration are intrinsically complex. Refactor with care.
- `lockdown` requires a dedicated service user (`lockdown_user`) and SSH keypair provisioning to run the CIS playbook isolated.

## Documentation

- [`AGENTS.md`](AGENTS.md) — developer conventions
- `roles/<role>/README.md` — per-role variable docs

## License

GPL-3.0-or-later
