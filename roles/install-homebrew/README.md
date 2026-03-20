Role Name
=========

This role installs Homebrew on Ubuntu/Debian and RHEL/CentOS/Fedora systems using the official installer script.

Requirements
------------

None - the role will install any required dependencies.

Role Variables
--------------

None - this role uses hardcoded values for the installation.

Dependencies
------------

None.

Example Playbook
----------------
You can set the environment variable to use the WFHT Roles using the following:

```bash
cd roles
export ANSIBLE_ROLES_PATH=`pwd`
```

The test playbook has the minimal tasks to complete the role given this example command:

```bash
ansible-playbook -K -i 192.168.0.22, -u wfht ~/projects/wfht-ansible/roles/install-homebrew/tests/test.yml
```
Requirements:  
This playbook assumes you have a shared ssh pub certificate to login to the host without a password.  

Options:
|Option|Description|
|------|-----------|
| -K   |This will prompt for the become password (superuser)|
| -i   |Provide a list of host IP addresses. NOTE the single , used with a single host|
| -u   |The user that has ssh access to the host(s)|

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: install-homebrew }

License
-------

BSD

Author Information
------------------

Assistance can be obtain at http://workfromhometech.io.
