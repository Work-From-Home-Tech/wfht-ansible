# Ansible Role: install-k3s

This Ansible role installs K3s, a lightweight Kubernetes distribution, on both master and worker nodes. Supports Debian/Ubuntu and RedHat/Rocky Linux systems.

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
[k3s_cluster]
MASTER ansible_host=192.168.1.10
WORKER1 ansible_host=192.168.1.11
WORKER2 ansible_host=192.168.1.12

[k3s_master]
MASTER

[k3s_workers]
WORKER1
WORKER2
```

Important notes about the inventory:
- The master node MUST be named 'MASTER' in the inventory (case-sensitive)
- Worker nodes can have any name, but should not be named 'MASTER'
- The master node must be accessible by all worker nodes on port 6443
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
    - install-k3s
```

## Installation Process

The role performs the following:
1. Installs required dependencies (curl, apt-transport-https, ca-certificates)
2. Installs K3s on the master node with:
   - Proper kubeconfig permissions
   - Node IP configuration using the inventory's ansible_host
   - API server bound to the node's IP instead of localhost
3. Retrieves the K3s token from the master node
4. Installs K3s on worker nodes and joins them to the cluster with:
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
1. The kubeconfig file will be available at `/etc/rancher/k3s/k3s.yaml` on the master node
2. K3s service will be running and enabled on all nodes
3. Worker nodes will be joined to the cluster automatically

## License

MIT

## Author Information

Created by WFHT
