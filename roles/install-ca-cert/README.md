# Ansible Role: install-ca-cert

This Ansible role installs a CA certificate on Ubuntu/Debian and RedHat-based systems.

## Requirements

- Ansible 2.9 or higher
- Root access on target systems

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `ca_cert_file` | The certificate file to install (relative to the role's `files` directory) | `my.certificate.com.crt.example` |

## Dependencies

None

## Example Playbook

Basic usage (uses the default example certificate):
```yaml
- hosts: servers
  roles:
    - role: install-ca-cert
```

Using your own certificate:
```yaml
- hosts: servers
  roles:
    - role: install-ca-cert
      vars:
        ca_cert_file: your-certificate.crt
```

Note: Place your certificate file in the role's `files` directory before running the playbook.

## License

MIT

## Author Information

Created by WFHT
