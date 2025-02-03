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
 
