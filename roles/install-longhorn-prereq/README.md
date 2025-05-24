# Ansible Role: install-longhorn-prereq

This role installs and configures all prerequisites required for Longhorn storage controller on Kubernetes clusters.

## Requirements

- Target nodes must be running a supported Linux distribution (Debian/Ubuntu or RHEL/CentOS)
- Root or sudo access on target nodes
- Ansible 2.9 or higher

## Role Variables

None

## Dependencies

None

## Prerequisites Installed

This role ensures the following prerequisites are installed and configured:

1. Storage Requirements:
   - Host filesystem must support file extents (ext4 or XFS)
   - Mount propagation enabled

2. Package Dependencies:
   - open-iscsi (Debian) / iscsi-initiator-utils (RedHat)
   - nfs-common (Debian) / nfs-utils (RedHat)
   - Required utilities:
     - bash
     - curl
     - findmnt
     - grep
     - awk
     - blkid
     - lsblk

3. Services:
   - iscsid daemon running and enabled

## Example Playbook

```yaml
- hosts: k8s_nodes
  roles:
    - install-longhorn-prereq
```

## Usage with K3s/RKE2

This role is designed to be used as a dependency in the install-k3s or install-rke2 roles to ensure all Longhorn prerequisites are met before installing the Kubernetes cluster.

## License

MIT

## Author Information

Created by Wendell
