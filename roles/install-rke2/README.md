# Ansible Role: install-rke2

This Ansible role installs RKE2 (Rancher Kubernetes Engine 2), a CNCF-certified Kubernetes distribution, on both master and worker nodes. It also installs the required filesystem packages to support Longhorn persistent storage. Supports Debian/Ubuntu and RedHat/Rocky Linux systems.

## Requirements

- Ansible 2.9 or higher
- Root access on target systems
- Properly configured inventory with master and worker nodes
- Supported operating systems:
  - Debian/Ubuntu
  - RedHat/Rocky Linux

## Role Variables

No variables are required as the role uses host groups to determine the installation type (master vs worker).

## Dependencies

None, but the following roles are recommended to be run first:
- update-packages
- install-docker

## Inventory Setup

Your inventory file should define the master and worker nodes. Example:

```ini
[rke2_cluster]
MASTER ansible_host=192.168.1.10
WORKER1 ansible_host=192.168.1.11
WORKER2 ansible_host=192.168.1.12

[rke2_master]
MASTER

[rke2_workers]
WORKER1
WORKER2
```

Important notes about the inventory:
- The master node MUST be named 'MASTER' in the inventory (case-sensitive)
- Worker nodes can have any name, but should not be named 'MASTER'
- The master node must be accessible by all worker nodes on ports 6443 and 9345
- Worker nodes will automatically join the cluster using the master's token

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - update-packages
    - install-docker

- hosts: all
  become: true
  roles:
    - install-rke2
```

## Installation Process

The role performs the following:
1. Installs required dependencies (curl, apt-transport-https, ca-certificates)
2. Installs filesystem packages for Longhorn support:
   - open-iscsi
   - nfs-common (Debian) / nfs-utils (RedHat)
   - xfsprogs
   - lvm2
3. Installs RKE2 on the master node with:
   - Proper kubeconfig permissions
   - Node IP configuration using the inventory's ansible_host
   - API server bound to the node's IP instead of localhost
4. Retrieves the RKE2 token from the master node
5. Installs RKE2 on worker nodes and joins them to the cluster with:
   - Proper node naming using inventory_hostname
   - Connection to master using master's ansible_host IP

### Network Configuration

The role automatically configures:
- Master node API server to bind to its ansible_host IP
- Worker nodes to connect to master using its ansible_host IP
- Each node is configured with its proper hostname from inventory

This ensures proper cluster networking and node communication.

## Post-Installation

After installation:
1. The kubeconfig file will be available at `/etc/rancher/rke2/rke2.yaml` on the master node
2. RKE2 service will be running and enabled on all nodes
3. Worker nodes will be joined to the cluster automatically
4. Longhorn prerequisites will be installed and configured
5. Reference Links:
   1. RKE2 - [https://docs.rke2.io](https://docs.rke2.io)
   2. Longhorn - [https://longhorn.io](https://longhorn.io)
   3. K9s - [https://github.com/derailed/k9s](https://github.com/derailed/k9s)
   4. Helm - [https://helm.sh](https://helm.sh)

## License

MIT

## Author Information

Created by WFHT
