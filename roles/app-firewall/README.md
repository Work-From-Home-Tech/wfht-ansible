# Ansible Role: app-firewall

This Ansible role configures system firewalls and hardens SSH access on both Debian/Ubuntu (using UFW) and RedHat-based systems (using firewalld).

## Requirements

- Ansible 2.9 or higher
- Root access on target systems
- Supported operating systems:
  - Debian/Ubuntu
  - RedHat/Rocky Linux/CentOS

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `allowed_tcp_ports` | List of TCP ports to allow through the firewall | `[22, 80, 443]` |
| `allowed_udp_ports` | List of UDP ports to allow through the firewall | `[51820]` |

## Dependencies

None

## Example Playbook

Basic usage with default settings:
```yaml
- hosts: servers
  become: true
  roles:
    - role: app-firewall
```

Customizing allowed ports:
```yaml
- hosts: servers
  become: true
  roles:
    - role: app-firewall
      vars:
        allowed_tcp_ports:
          - 22   # SSH
          - 80   # HTTP
          - 443  # HTTPS
          - 8080 # Custom application
        allowed_udp_ports:
          - 51820 # WireGuard VPN
          - 53    # DNS
```

## Installation Process

The role performs the following:

1. Installs the appropriate firewall package:
   - UFW on Debian/Ubuntu systems
   - firewalld on RedHat-based systems

2. Configures the firewall to:
   - Allow incoming traffic on specified TCP ports (default: 22, 80, 443)
   - Allow incoming traffic on specified UDP ports (default: 51820)
   - Allow all outgoing traffic
   - Deny all other incoming traffic

3. Hardens SSH configuration:
   - Disables password authentication
   - Disables challenge-response authentication
   - Enables public key authentication only

4. Ensures the firewall service is started and enabled at boot

## Security Considerations

This role implements several security best practices:
- Restricts SSH access to public key authentication only
- Follows the principle of least privilege by only opening necessary ports
- Enables firewall by default with a deny-all policy for incoming traffic

## License

MIT

## Author Information

Created by WFHT
