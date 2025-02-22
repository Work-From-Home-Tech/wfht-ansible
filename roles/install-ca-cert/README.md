# Ansible Role: install-ca-cert

This Ansible role installs a CA certificate on Ubuntu/Debian and RedHat-based systems.

## Requirements

- Ansible 2.9 or higher
- Root access on target systems

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `ca_cert_file` | The certificate file to install (relative to the role's `files` directory) | `my.certificate.com.crt.example` |
| `ca_cert_path` | Full path to certificate file (takes precedence over `ca_cert_file`) | `""` |

## Dependencies

None

## Example Playbook

Basic usage (uses the default example certificate):
```yaml
- hosts: servers
  roles:
    - role: install-ca-cert
```

Using a certificate from the role's files directory:
```yaml
- hosts: servers
  roles:
    - role: install-ca-cert
      vars:
        ca_cert_file: your-certificate.crt
```

Using a certificate from any location (command line):
```bash
ansible-playbook playbook.yml -e "ca_cert_path=/path/to/your/certificate.crt"
```

Using a certificate from any location (in playbook):
```yaml
- hosts: servers
  roles:
    - role: install-ca-cert
      vars:
        ca_cert_path: /path/to/your/certificate.crt
```

Notes:
- When using `ca_cert_file`, place your certificate in the role's `files` directory
- When using `ca_cert_path`, specify the full path to your certificate file
- `ca_cert_path` takes precedence over `ca_cert_file` if both are specified

## License

MIT

## Author Information

Created by WFHT
