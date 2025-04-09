# Ansible Role: install-golang

This Ansible role installs and configures Go (Golang) programming language on Linux systems. It provides options for installing specific versions, setting up the Go workspace, and configuring environment variables.

## Requirements

- Ansible 2.1 or higher
- Root access on target systems
- Supported operating systems:
  - Debian/Ubuntu
  - RedHat/CentOS/Rocky Linux

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `golang_version` | Go version to install | `1.21.0` |
| `golang_download_location` | Temporary download location | `/tmp` |
| `golang_install_dir` | Installation directory | `/usr/local` |
| `golang_gopath` | GOPATH directory | `$HOME/go` |
| `golang_bin_path` | Add Go binaries to PATH | `true` |
| `golang_remove_tarball` | Remove the tarball after installation | `true` |
| `golang_install_profile` | Whether to add Go environment variables to profile | `true` |
| `golang_users` | List of users to configure Go environment for | `[]` |

## Dependencies

None

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  roles:
    - role: install-golang
```

Installing a specific version:
```yaml
- hosts: servers
  become: true
  vars:
    golang_version: "1.20.7"
  roles:
    - role: install-golang
```

Advanced configuration:
```yaml
- hosts: servers
  become: true
  vars:
    golang_version: "1.21.0"
    golang_install_dir: "/opt/go"
    golang_gopath: "/opt/go-workspace"
    golang_users:
      - username: developer1
        gopath: "/home/developer1/projects/go"
      - username: developer2
  roles:
    - role: install-golang
```

## Installation Process

The role performs the following:

1. Downloads the specified Go version from the official website
2. Extracts the archive to the installation directory
3. Sets up environment variables (GOROOT, GOPATH, PATH)
4. Configures user profiles with Go environment settings
5. Creates the GOPATH directory structure if it doesn't exist

## Verification

After installation, you can verify Go is installed correctly by:

```bash
$ go version
go version go1.21.0 linux/amd64
```

## Workspace Structure

The role sets up the standard Go workspace structure:

```
$GOPATH/
├── bin/    # Compiled binaries
├── pkg/    # Package objects
└── src/    # Source code
```

## License

MIT

## Author Information

Created by WFHT
