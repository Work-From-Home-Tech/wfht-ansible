# Ansible Role: install-lxd

This Ansible role installs and configures LXD (Linux Container Daemon) on Ubuntu and RedHat-based systems.

## Requirements

- Ubuntu 20.04+ or RedHat/CentOS 8+
- Systemd
- Sufficient storage space for the LXD storage pool

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Storage configuration
lxd_storage_backend: "dir"  # Options: dir, zfs, btrfs
lxd_storage_pool_name: "default"
lxd_storage_pool_size: "5GB"  # Only used for zfs/btrfs

# Network configuration
lxd_bridge_name: "lxdbr0"
lxd_bridge_ipv4_addr: "10.0.0.1/24"
lxd_bridge_ipv4_dhcp: true
lxd_bridge_ipv4_dhcp_range: "10.0.0.2,10.0.0.254"
lxd_bridge_ipv6_enabled: false

# Security
lxd_trust_password: ""  # Set this for remote access

# Users to add to lxd group
lxd_users: ["{{ ansible_user }}"]
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: install-lxd
      vars:
        lxd_storage_backend: "zfs"
        lxd_storage_pool_size: "10GB"
        lxd_users: ["myuser"]
```

## License

MIT

## Author Information

Created in 2025
