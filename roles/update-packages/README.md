# Ansible Role: update-packages

This Ansible role updates system packages on Debian/Ubuntu and RedHat-based systems. It handles package cache updates, package installations, and cleanup operations.

## Requirements

- Ansible 2.9 or higher
- Root access on target systems
- Supported operating systems:
  - Ubuntu 18.04 (Bionic), 20.04 (Focal), 22.04 (Jammy)
  - RedHat/Rocky Linux/CentOS 8, 9

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `packages` | List of packages to install/update | `['python3-pip', 'git']` |
| `update_cache_valid_time` | How long (in seconds) the apt cache is considered valid | `3600` |
| `autoremove` | Whether to remove unused packages | `true` |
| `autoclean` | Whether to clean package cache (Debian/Ubuntu only) | `true` |

## Dependencies

None

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  roles:
    - role: update-packages
```

Customizing packages to update:
```yaml
- hosts: servers
  become: true
  vars:
    packages:
      - python3-pip
      - git
      - curl
      - vim
      - htop
    autoremove: false
  roles:
    - role: update-packages
```

## Installation Process

The role performs the following:

1. Updates package cache:
   - On Debian/Ubuntu: `apt update`
   - On RedHat: `dnf makecache`

2. Updates specified packages to latest versions:
   - On Debian/Ubuntu: `apt upgrade`
   - On RedHat: `dnf update`

3. Performs cleanup operations (if enabled):
   - On Debian/Ubuntu: `apt autoremove` and `apt autoclean`
   - On RedHat: `dnf autoremove`

## Usage Notes

- This role is often used as a first step in playbooks to ensure systems are up-to-date before installing additional software
- The default package list includes `python3-pip` and `git`, which are commonly needed for other roles
- The role is designed to be idempotent and can be run repeatedly without issues

## License

MIT

## Author Information

Created by Wendell Jefferson
