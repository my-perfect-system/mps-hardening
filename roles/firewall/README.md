---
namespace: mps
collection: hardening
role: firewall
---

# `mps.hardening.firewall`

Render iptables rules.v4 and install systemd restore service

## Default variables

| Variable | Default | Description |
|---|---|---|
| `firewall_enable_icmp` | `true` | ACCEPT ICMP on INPUT and OUTPUT |
| `firewall_enable_nat_ip_forwarding` | `false` | Enable IPv4 forwarding + NAT masquerade (off by default) |
| `firewall_nat_out_interface` | `` | WAN interface for NAT masquerade (required when firewall_enable_nat_ip_forwarding is true) |
| `firewall_nat_source_network` | `` | Source network CIDR for NAT masquerade (required when firewall_enable_nat_ip_forwarding is true) |
| `firewall_packages` | `- iptables` | Apt packages required for iptables |
| `firewall_policies` | `{ input: …, output: …, forward: … }` | Default chain policies (keys: input, output, forward) |
| `firewall_rules_dir` | `/etc/iptables` | Directory where rules.v4 is written |
| `firewall_rules_path` | `{{ firewall_rules_dir }}/rules.v4` | Full path to the rendered rules file |
| `firewall_service_name` | `iptables` | systemd service name (the unit that calls iptables-restore on boot) |
| `firewall_service_path` | `/etc/systemd/system/{{ firewall_service_name }}.service` | Full path to the systemd unit file |
| `firewall_tcp_ports` | `- '22'` | TCP destination ports to ACCEPT in NEW state on INPUT |
| `firewall_udp_ports` | `[]` | UDP destination ports to ACCEPT in NEW state on INPUT |

## Dependencies

None.

## Example usage

```yaml
- hosts: all
  roles:
    - mps.hardening.firewall
```

## Role metadata

- **Min Ansible version**: `2.16.0`
- **License**: GPL-3.0-or-later
- **Platforms**: Debian (trixie)
- **Tasks file lines**: 51

## Related files

- [`meta/main.yml`](meta/main.yml) — galaxy_info + role dependencies
- [`meta/argument_specs.yml`](meta/argument_specs.yml) — variable spec (the source of the variable table above)
- [`defaults/main.yml`](defaults/main.yml) — variable defaults (the source of the default values above)
