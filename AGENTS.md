# AGENTS.md — odem-hardening

System-level security hardening — firewall (iptables), apparmor
profiles, auditd config + handler, AIDE intrusion detection, CIS
lockdown (clones the `ansible-lockdown/DEBIAN13-CIS` playbook and
runs it as a different user).

## Galaxy

- **namespace**: `odem`
- **name**: `hardening`
- **version**: `0.3.1`
- **dependencies**: `odem.base >=0.1.0`, `ansible.posix >=1.0.0`, `community.crypto >=2.0.0`

## Roles

| Role | Description | Complexity |
|---|---|---|
| `odem.hardening.firewall` | iptables rules.v4.j2 with 2 for-loops + 2 if-blocks (port ranges, ICMP, NAT). sysctl reload gated by `firewall_enable_nat_ip_forwarding`. Systemd unit template for the iptables-restore service. | 3 (accepted) |
| `odem.hardening.apparmor` | Install apparmor-utils, `synchronize` profiles from role `files/`, enforce + restart. | 1 |
| `odem.hardening.auditd` | apt install, 2 dir ensures (rules.d + run), 2 templates (`/etc/audit/auditd.conf` with ~13 vars, systemd override from `files/`). | 2 |
| `odem.hardening.aide` | apt install, `/var/lib/aide` directory, render one small static template. | 1 |
| `odem.hardening.lockdown` | Install `cracklib-runtime` + `ansible`, clone `DEBIAN13-CIS` to `/usr/share/mps/lockdown/`, generate SSH keypair + authorized_key, 5 regex `lineinfile` overrides into the CIS defaults, sub-playbook invocation gated by `lockdown_enable_execute`. | 3 (accepted) |

## Conventions

- All roles are system-level (no per-user logic, no `odem_filter_users`).
- `firewall` and `lockdown` complexity is load-bearing — their templates / external-repo orchestration are intrinsically complex. Do not refactor.
- `apparmor` profile files live in `roles/apparmor/files/etc/apparmor.d/` and are `synchronize`'d onto the target. Mode/owner set explicitly.
- `lockdown` runs the CIS playbook as `{{ lockdown_user }}` (typically a non-root service user) with `become_user: true`.
