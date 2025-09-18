# Install Fastfetch

This Ansible role installs the fastfetch system information tool from the official GitHub releases. Fastfetch is a neofetch-like tool for fetching system information and displaying it in a pretty way.

## Requirements

- Ansible 2.9 or higher
- Internet connectivity to download packages from GitHub
- Supported operating systems:
  - Ubuntu (all versions)
  - Debian (all versions)
  - RHEL/CentOS/Rocky Linux 7, 8, 9

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# GitHub API URL for latest release
fastfetch_github_api_url: "https://api.github.com/repos/fastfetch-cli/fastfetch/releases/latest"

# Temporary directory for downloads
fastfetch_temp_dir: "/tmp"

# Whether to clean up downloaded packages after installation
fastfetch_cleanup_downloads: true

# Package architecture (currently only amd64 is supported)
fastfetch_architecture: "amd64"
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  become: yes
  roles:
    - install-fastfetch
```

## Example with custom variables

```yaml
- hosts: servers
  become: yes
  roles:
    - role: install-fastfetch
      vars:
        fastfetch_cleanup_downloads: false
        fastfetch_temp_dir: "/var/tmp"
```

## What this role does

1. Detects the operating system family (Debian/Ubuntu or RedHat/CentOS)
2. Queries the GitHub API to get the latest fastfetch release information
3. Downloads the appropriate package (.deb for Debian/Ubuntu, .rpm for RHEL/CentOS)
4. Installs the package using the system package manager (with GPG signature checking disabled for RPM packages since they're not signed)
5. Verifies the installation by running `fastfetch --version`
6. Optionally cleans up the downloaded package file

## Supported Packages

- **Debian/Ubuntu**: `fastfetch-linux-amd64.deb`
- **RHEL/CentOS/Rocky**: `fastfetch-linux-amd64.rpm`

## License

MIT

## Author Information

This role was created by Wendell Jefferson as part of the WFHT Ansible collection.
