# Ansible Role: install-kvm

This Ansible role installs and configures KVM (Kernel-based Virtual Machine) on Ubuntu and RedHat-based systems.

## Requirements

- Ubuntu or RedHat-based Linux distribution
- CPU with virtualization support (Intel VT-x or AMD-V)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Default user to add to libvirt group
kvm_user: "{{ ansible_user }}"
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: install-kvm
      vars:
        kvm_user: "myuser"
```

## License

MIT

## Author Information

Created for WorkFromHomeTech in 2025
