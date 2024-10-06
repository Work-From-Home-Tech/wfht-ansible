Role Name
=========

This role is to be used by any linux system that needs the official docker release installed. Currently it only supports Ubuntu but will ultimatly support Ubuntu/Debian and RHEL/Rocky variants.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
You can set the environment variable to use the WFHT Roles using the following:

```bash
cd roles
export ANSIBLE_ROLES_PATH=`pwd`
```

The test playbook has the minimal tasks to complete the role given this example command:

```bash
ansible-playbook -K -i 192.168.0.22, -u wfht ~/projects/wfht-ansible/roles/install-docker/tests/test.yml
```
Requirements:  
This playbook assumes you have a shared ssh pub certficate to login to the host without a password.  

Options:
|Option|Description|
|------|-----------|
| -K   |This will prompt for the become password (superuser)|
| -i   |Provide a list of host IP addresses. NOTE the single , used with a single host|
| -u   |The user that has ssh access to the host(s)|

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

Assistance can be obtain at http://workfromhometech.io.
