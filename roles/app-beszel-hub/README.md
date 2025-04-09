# Ansible Role: app-beszel-hub

This Ansible role deploys Beszel Hub, a monitoring and management solution for Docker environments, using Docker Compose. The role sets up both the Beszel Hub server and the Beszel agent for collecting metrics from the host system.

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
    compose_dir: "/opt/beszel"
  roles:
    - role: install-docker
    - role: app-beszel-hub
```

## Installation Process

The role performs the following:

1. Creates the specified directory for Docker Compose files
2. Copies the Docker Compose configuration to the target system
3. Starts the Beszel Hub and agent containers using Docker Compose

## Deployed Services

### Beszel Hub
- Container name: `beszel`
- Port: 8090
- Persistent data stored in `./beszel_data` within the compose directory
- Web interface accessible at http://[server-ip]:8090

### Beszel Agent
- Container name: `beszel-agent`
- Runs in host network mode
- Monitors the Docker host
- Collects system metrics and Docker container information
- Communicates with the Beszel Hub

## Configuration Notes

- The agent requires access to the Docker socket to monitor containers
- The default agent port is 45876
- You may need to configure the `KEY` environment variable in the compose file for secure communication
- For disk I/O statistics, uncomment and set the `FILESYSTEM` environment variable in the compose file

## License

MIT

## Author Information

Created by WFHT
