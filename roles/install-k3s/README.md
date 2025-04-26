# Ansible Role: install-k3s

This Ansible role installs K3s, a lightweight Kubernetes distribution, with high availability (HA) control plane support. It configures both master and worker nodes, supporting Debian/Ubuntu and RedHat/Rocky Linux systems.

## Requirements

- Ansible 2.9 or higher
- Root access on target systems
- Properly configured inventory with master and worker nodes
- Minimum of 3 master nodes for HA control plane
- Minimum of 2 worker nodes recommended (1+ required)
- Supported operating systems:
  - Debian/Ubuntu
  - RedHat/Rocky Linux

## Role Variables

The role provides several variables that can be customized:

| Variable | Description | Default |
|----------|-------------|---------|
| k3s_token_file | Location of the node token file | /var/lib/rancher/k3s/server/node-token |
| k3s_kubeconfig_file | Location of the kubeconfig file | /etc/rancher/k3s/k3s.yaml |
| k3s_kubeconfig_mode | File permissions for kubeconfig | "644" |
| k3s_ha_enabled | Enable HA control plane | true |
| k3s_primary_master | Primary master node name | First node in k3s_masters group |
| k3s_server_args_common | Common server arguments | Node IP configuration |
| k3s_server_args_primary | Primary server arguments | Common args + cluster-init |
| k3s_server_args_secondary | Secondary server arguments | Common args + server URL |

## Dependencies

None, but the following roles are recommended to be run first:
- update-packages
- install-docker

## Inventory Setup

Your inventory file should define the master and worker nodes. Example for HA setup:

```ini
[k3s_cluster]
MASTER1 ansible_host=192.168.1.10
MASTER2 ansible_host=192.168.1.11
MASTER3 ansible_host=192.168.1.12
WORKER1 ansible_host=192.168.1.13
WORKER2 ansible_host=192.168.1.14

[k3s_masters]
MASTER1
MASTER2
MASTER3

[k3s_workers]
WORKER1
WORKER2
```

Important notes about the inventory:
- The first node in the k3s_masters group will be used as the primary master
- All master nodes must be accessible by other nodes on port 6443
- Worker nodes will automatically join the cluster using the primary master's token
- All nodes should have unique hostnames

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
2. Installs K3s on the primary master node with:
   - Cluster initialization flag (--cluster-init)
   - Embedded etcd for HA control plane
   - Proper kubeconfig permissions
   - Node IP configuration using the inventory's ansible_host
   - API server bound to the node's IP
3. Retrieves the K3s token from the primary master node
4. Installs K3s on secondary master nodes and joins them to the cluster with:
   - Server URL pointing to the primary master
   - Same token as the primary master
   - Node IP configuration using the inventory's ansible_host
5. Installs K3s on worker nodes and joins them to the cluster with:
   - Proper node naming using inventory_hostname
   - Connection to primary master using its ansible_host IP

### High Availability Architecture

The HA setup uses K3s's embedded etcd database for control plane coordination:
- The primary master initializes the cluster with `--cluster-init`
- Secondary masters join the cluster as additional control plane nodes
- The etcd cluster automatically forms between the master nodes
- If the primary master fails, the cluster continues to operate
- API requests can be made to any master node

### Network Configuration

The role automatically configures:
- All master nodes' API servers to bind to their ansible_host IP
- Worker nodes to connect to the primary master using its ansible_host IP
- Each node is configured with its proper hostname from inventory

This ensures proper cluster networking and node communication.

## Post-Installation

After installation:
1. The kubeconfig file will be available at `/etc/rancher/k3s/k3s.yaml` on all master nodes
2. K3s service will be running and enabled on all nodes
3. The cluster will have a highly available control plane that can survive master node failures
4. For external access, consider setting up a load balancer in front of all master nodes
5. Reference Links:
   1. K3s - [https://k3s.io](https://k3s.io)  
   2. K3s HA - [https://docs.k3s.io/datastore/ha](https://docs.k3s.io/datastore/ha)
   3. K9s - [https://github.com/derailed/k9s](https://github.com/derailed/k9s)  
   4. Tools - [https://kubernetes.io/docs/tasks/tools](https://kubernetes.io/docs/tasks/tools)  
   5. Helm - [https://helm.sh](https://helm.sh)

## License

MIT

## Author Information

Created by WFHT
