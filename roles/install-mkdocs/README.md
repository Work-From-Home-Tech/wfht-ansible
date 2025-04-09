# Ansible Role: install-mkdocs

This Ansible role installs and configures MkDocs, a fast and simple static site generator designed for building project documentation. The role supports installation of MkDocs and popular themes/plugins, as well as initial project setup.

## Requirements

- Ansible 2.1 or higher
- Python 3.6 or higher
- pip (Python package manager)
- Supported operating systems:
  - Debian/Ubuntu
  - RedHat/CentOS/Rocky Linux

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `mkdocs_version` | MkDocs version to install | `latest` |
| `mkdocs_install_method` | Installation method (pip, pipx, system) | `pip` |
| `mkdocs_user` | User to install MkDocs for (empty for system-wide) | `""` |
| `mkdocs_group` | Group for the MkDocs user | `""` |
| `mkdocs_venv_path` | Path to virtual environment (if using) | `""` |
| `mkdocs_install_dir` | Directory for MkDocs projects | `/opt/mkdocs` |
| `mkdocs_create_project` | Whether to create an initial project | `false` |
| `mkdocs_project_name` | Name of the initial project | `docs` |
| `mkdocs_theme` | Theme to use | `mkdocs` |
| `mkdocs_plugins` | List of plugins to install | `[]` |
| `mkdocs_serve` | Whether to start the development server | `false` |
| `mkdocs_serve_port` | Port for the development server | `8000` |
| `mkdocs_serve_host` | Host for the development server | `127.0.0.1` |

## Dependencies

None

## Example Playbook

Basic installation:
```yaml
- hosts: servers
  become: true
  roles:
    - role: install-mkdocs
```

Installing with Material theme and plugins:
```yaml
- hosts: servers
  become: true
  vars:
    mkdocs_theme: "material"
    mkdocs_plugins:
      - search
      - minify
      - git-revision-date-localized
      - mkdocstrings
  roles:
    - role: install-mkdocs
```

Creating a new project:
```yaml
- hosts: servers
  become: true
  vars:
    mkdocs_create_project: true
    mkdocs_project_name: "my-documentation"
    mkdocs_install_dir: "/var/www/docs"
    mkdocs_theme: "material"
  roles:
    - role: install-mkdocs
```

## Installation Process

The role performs the following:

1. Installs Python and pip if not already present
2. Installs MkDocs using the specified method (pip, pipx, or system package)
3. Installs the specified theme and plugins
4. Creates the installation directory with proper permissions
5. Initializes a new MkDocs project if requested
6. Configures the project with the specified theme and plugins
7. Optionally starts the development server

## MkDocs Configuration

The role creates a basic `mkdocs.yml` configuration file with:

```yaml
site_name: Your Project Name
theme: chosen_theme
plugins:
  - specified_plugins
```

## Available Themes

The role supports installing various themes including:
- mkdocs (default)
- material
- readthedocs
- cinder
- windmill

## Common Plugins

Some useful plugins that can be installed:
- search (included by default)
- minify (reduces HTML/CSS/JS file size)
- git-revision-date-localized (shows last update date)
- mkdocstrings (auto-documentation from docstrings)
- pdf-export (exports documentation as PDF)

## License

MIT

## Author Information

Created by WFHT
