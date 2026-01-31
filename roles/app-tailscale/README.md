app-tailscale
=============

This is a simplified install of the Tailscale service on a node. If you are looking for a more robust ansible role for Tailscale then this repo might be best for you:
[https://github.com/artis3n/ansible-role-tailscale](https://github.com/artis3n/ansible-role-tailscale)

This role supports Debian, Ubuntu, CentOS, RHEL, Fedora, Arch, and openSUSE hosts.

Requirements
------------

- A Tailscale account
- A Tailscale auth key or OAuth client secret (generate at https://login.tailscale.com/admin/settings/keys)

Role Variables
--------------

### Required Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `tailscale_authkey` | Tailscale auth key or OAuth client secret for node authentication. Can be passed via extra vars, host/group vars, or Ansible Vault. | `tskey-auth-ADD_YOUR_KEY_HERE` |

### Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `state` | Whether to install or uninstall Tailscale. Options: `latest`, `present`, `absent` | `latest` |
| `tailscale_args` | Additional command-line arguments for `tailscale up` | `""` |
| `tailscale_tags` | List of tags to apply to the node (required when using OAuth keys) | `[]` |
| `tailscale_up_timeout` | Timeout in seconds for `tailscale up` command | `120` |
| `tailscale_up_skip` | Skip running `tailscale up` (install only) | `false` |
| `release_stability` | Use `stable` or `unstable` Tailscale builds | `stable` |
| `verbose` | Output debug information during role execution | `false` |

### OAuth-specific Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `tailscale_oauth_ephemeral` | Register as an ephemeral node (recommended for OAuth) | `true` |
| `tailscale_oauth_preauthorized` | Skip manual device approval | `false` |

Dependencies
------------

None.

Example Playbook
----------------

### Basic usage with inline variable

```yaml
- hosts: servers
  roles:
    - role: app-tailscale
      tailscale_authkey: "tskey-auth-xxxxx"
```

### Using extra vars (recommended for CI/CD)

```bash
ansible-playbook playbook.yml -e "tailscale_authkey=tskey-auth-xxxxx"
```

### Using Ansible Vault (recommended for secrets)

Create an encrypted vars file:

```bash
ansible-vault create group_vars/all/vault.yml
```

Add your authkey:

```yaml
tailscale_authkey: "tskey-auth-xxxxx"
```

Then run your playbook:

```bash
ansible-playbook playbook.yml --ask-vault-pass
```

### Using OAuth with tags

```yaml
- hosts: servers
  roles:
    - role: app-tailscale
      tailscale_authkey: "tskey-client-xxxxx"
      tailscale_tags:
        - webserver
        - production
```

License
-------

BSD
