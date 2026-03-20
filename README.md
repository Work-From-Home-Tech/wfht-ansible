# Work From Home Tech Useful Ansible
Work from home tech ansible roles and playbooks.

## Roles

Container roles will always install as docker compose files in the /opt/stacks directory for compatability with dockage prefered usage. This makes things easily consistent and accessible from the Dockage GUI.

## Using wfht-ansible
1) Clone the wfh-ansible repository
2) Add the wfht-ansible/roles directory to your $HOME/.ansible/ansible.cfg file role path
   ex. roles_path=/home/user/wfht-ansible/roles  
   or use the ANSIBLE_ROLES_PATH environment variable.  
   The playbooks in the root directory have been setup to function as is and are compatible with Semaphore operations.  
3) Use the test file for each role as an example playbook

### Playbooks

docker-tailscale.yml - Installs Docker-CE engine and tailscale. You will have to provide a node token within the role.    
update_packages.yml - Updates all packages on Ubuntu and Red Hat nodes.

## Available Roles

### Infrastructure & Platform Roles
- [install-docker](roles/install-docker/README.md) - Docker CE installation
- [install-k3s](roles/install-k3s/README.md) - Lightweight Kubernetes (K3s) cluster setup
- [install-rke2](roles/install-rke2/README.md) - RKE2 Kubernetes cluster with Longhorn storage
- [install-longhorn-prereq](roles/install-longhorn-prereq/README.md) - Longhorn storage prerequisites
- [install-docker-swarm](roles/install-docker-swarm/README.md) - Docker Swarm cluster setup
- [install-kvm](roles/install-kvm/README.md) - KVM virtualization platform
- [install-lxd](roles/install-lxd/README.md) - LXD container platform

### Application Deployment Roles
- [app-beszel-hub](roles/app-beszel-hub/README.md) - Beszel Hub deployment
- [app-paperless-ngx](roles/app-paperless-ngx/README.md) - Paperless-ngx document management
- [app-wordpress](roles/app-wordpress/README.md) - WordPress deployment
- [app-tailscale](roles/app-tailscale/README.md) - Tailscale VPN setup
- [install-authentik](roles/install-authentik/README.md) - Authentik identity management
- [install-chatbot](roles/install-chatbot/README.md) - Chat bot service deployment

### Development Tools
- [install-golang](roles/install-golang/README.md) - Go language installation
- [install-mkdocs](roles/install-mkdocs/README.md) - MkDocs documentation tool
- [install-caddy](roles/install-caddy/README.md) - Caddy web server
- [install-homebrew](roles/install-homebrew/README.md) - Homebrew package manager installation

### System Management
- [update-packages](roles/update-packages/README.md) - System package updates
- [app-firewall](roles/app-firewall/README.md) - Firewall management
- [install-ca-cert](roles/install-ca-cert/README.md) - CA certificate installation
- [install-fastfetch](roles/install-fastfetch/README.md) - Fastfetch system information tool
