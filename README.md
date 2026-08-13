# `odem.hardening` Ansible Collection

System-level security hardening — firewall (iptables), apparmor
profiles, auditd, AIDE intrusion detection, CIS lockdown (clones
`ansible-lockdown/DEBIAN13-CIS`).

## Galaxy metadata

- **namespace**: `odem`
- **name**: `hardening`
- **version**: `0.3.1`
- **dependencies**: `odem.base`, `ansible.posix`, `community.crypto`

See [`galaxy.yml`](galaxy.yml) for the canonical values.

## Roles

| Role | Purpose |
|---|---|
| [`odem.hardening.firewall`](roles/firewall/README.md) | iptables rules (templated with port ranges, ICMP, NAT). |
| [`odem.hardening.apparmor`](roles/apparmor/README.md) | Apparmor profile sync + enforce. |
| [`odem.hardening.auditd`](roles/auditd/README.md) | auditd + auditd.conf + systemd override. |
| [`odem.hardening.aide`](roles/aide/README.md) | AIDE intrusion detection. |
| [`odem.hardening.lockdown`](roles/lockdown/README.md) | DEBIAN13-CIS clone + sub-playbook invocation (gated by `lockdown_enable_execute`). |
| [`odem.hardening.fail2ban`](roles/fail2ban/README.md) | Fail2ban with default sshd jail to prevent SSH brute-force attacks. |

## Installation

```bash
ansible-galaxy collection install odem.hardening
ansible-galaxy collection install community.crypto
```

## Usage

```yaml
- hosts: all
  become: true
  roles:
    - odem.hardening.firewall
    - odem.hardening.apparmor
    - odem.hardening.auditd
    - odem.hardening.aide
    - odem.hardening.lockdown
    - odem.hardening.fail2ban
```

## Caveats

- `firewall` and `lockdown` complexity is load-bearing — the templates and external-repo orchestration are intrinsically complex. Refactor with care.
- `lockdown` requires a dedicated service user (`lockdown_user`) and SSH keypair provisioning to run the CIS playbook isolated.

## Documentation

- [`AGENTS.md`](AGENTS.md) — developer conventions
- `roles/<role>/README.md` — per-role variable docs

## License

GPL-3.0-or-later
