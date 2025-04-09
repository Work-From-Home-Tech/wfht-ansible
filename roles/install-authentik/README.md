# Ansible Role: install-authentik

This Ansible role installs and configures Authentik, an open-source Identity Provider (IdP) that provides flexible authentication, authorization, and user management capabilities.

## Requirements

- Ansible 2.1 or higher
- Docker and Docker Compose (recommended for deployment)
- PostgreSQL database (can be deployed as part of the role)
- Redis (can be deployed as part of the role)

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `authentik_version` | Version of Authentik to install | `latest` |
| `authentik_domain` | Domain name for Authentik | `authentik.example.com` |
| `authentik_secret_key` | Secret key for Authentik | Generated randomly |
| `authentik_postgres_password` | PostgreSQL password | Generated randomly |
| `authentik_postgres_user` | PostgreSQL username | `authentik` |
| `authentik_postgres_db` | PostgreSQL database name | `authentik` |
| `authentik_admin_email` | Admin email address | `admin@example.com` |
| `authentik_admin_password` | Admin password | Generated randomly |
| `authentik_install_dir` | Installation directory | `/opt/authentik` |
| `authentik_port` | Port for the web interface | `9000` |
| `authentik_secure` | Enable HTTPS | `true` |

## Dependencies

- Requires Docker to be installed (recommend using the `install-docker` role first)

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  vars:
    authentik_domain: "auth.yourdomain.com"
    authentik_admin_email: "admin@yourdomain.com"
  roles:
    - role: install-docker
    - role: install-authentik
```

Advanced configuration:
```yaml
- hosts: servers
  become: true
  vars:
    authentik_domain: "auth.yourdomain.com"
    authentik_admin_email: "admin@yourdomain.com"
    authentik_admin_password: "securepassword"
    authentik_version: "2023.8.3"
    authentik_port: 8000
    authentik_install_dir: "/data/authentik"
  roles:
    - role: install-docker
    - role: install-authentik
```

## Installation Process

The role performs the following:

1. Creates the necessary directories for Authentik
2. Generates secure passwords if not provided
3. Sets up a Docker Compose configuration for Authentik
4. Deploys the Authentik containers (server, worker, PostgreSQL, Redis)
5. Configures the initial admin user
6. Sets up the web interface

## Features

- Single Sign-On (SSO) for web applications
- Multi-factor authentication (MFA)
- Social login providers (Google, GitHub, etc.)
- User self-service portal
- Password policies and account recovery
- SAML, OAuth2, and LDAP support
- Customizable login flows and branding
- API for integration with other systems

## Security Considerations

- Use a strong admin password
- Enable HTTPS for production deployments
- Regularly update Authentik to receive security patches
- Consider using a dedicated database server for production
- Backup the database regularly

## License

MIT

## Author Information

Created by WFHT
