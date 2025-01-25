# Ansible Role: install-caddy

This role installs and configures Caddy web server with support for importing host configurations from `/etc/caddy/caddyfile.d/`.

## Requirements

- Ubuntu or RedHat/Rocky Linux
- Ansible 2.9 or higher

## Role Variables

Available variables are listed below, along with default values:

```yaml
caddy_user: "caddy"
caddy_group: "caddy"
caddy_config_dir: "/etc/caddy"
caddy_config_d_dir: "/etc/caddy/caddyfile.d"
caddy_service_enabled: true
caddy_service_state: "started"
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: install-caddy
```

## License

MIT

## Author Information

Created by WFHT Ansible Project
