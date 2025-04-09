# Ansible Role: app-wordpress

This Ansible role deploys WordPress using Docker Compose, setting up both the WordPress application and a MySQL database with persistent storage.

## Requirements

- Ansible 2.1 or higher
- Docker installed on the target system
- Docker Compose installed on the target system

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `compose_dir` | Directory where the Docker Compose file will be placed | Required, no default |

## Dependencies

- Requires Docker to be installed (recommend using the `install-docker` role first)

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  vars:
    compose_dir: "/opt/wordpress"
  roles:
    - role: install-docker
    - role: app-wordpress
```

## Installation Process

The role performs the following:

1. Creates the specified directory for Docker Compose files
2. Copies the Docker Compose configuration to the target system
3. Starts the WordPress and MySQL containers using Docker Compose

## Deployed Services

### WordPress
- Container: WordPress official image
- Port: 8080 (accessible at http://[server-ip]:8080)
- Persistent storage for WordPress files
- Default admin interface at http://[server-ip]:8080/wp-admin

### MySQL Database
- Container: MySQL 8.0
- Not exposed to the host network
- Persistent storage for database files
- Pre-configured with WordPress database and user

## Configuration Notes

- Default database name: `wordpress`
- Default database user: `wfht`
- Default database password: `WVn8lM7d8yTafbXHKw8GEQFyAmk=`
- MySQL root password is randomly generated for security

## Security Considerations

- The default database credentials should be changed for production use
- Consider using a reverse proxy with HTTPS for production deployments
- Regularly update the WordPress and MySQL images to receive security patches

## Post-Installation

After installation:
1. Access WordPress at http://[server-ip]:8080
2. Complete the WordPress setup wizard
3. Install necessary plugins and themes
4. Configure WordPress settings as needed

## License

MIT

## Author Information

Created by Wendell Jefferson, Work From Home Tech
