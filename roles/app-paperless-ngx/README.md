# Ansible Role: app-paperless-ngx

This Ansible role deploys Paperless-ngx, a document management system that helps digitize and organize paper documents. Paperless-ngx provides a web interface for uploading, viewing, and searching documents, with OCR capabilities to make scanned documents searchable.

## Requirements

- Ansible 2.1 or higher
- Docker and Docker Compose (recommended for deployment)
- Sufficient storage space for document storage

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `paperless_data_dir` | Directory for Paperless-ngx data storage | `/opt/paperless/data` |
| `paperless_media_dir` | Directory for document storage | `/opt/paperless/media` |
| `paperless_export_dir` | Directory for document exports | `/opt/paperless/export` |
| `paperless_consume_dir` | Directory for document consumption | `/opt/paperless/consume` |
| `paperless_port` | Port for the web interface | `8000` |
| `paperless_admin_user` | Admin username | `admin` |
| `paperless_admin_password` | Admin password | `adminpassword` |
| `paperless_admin_email` | Admin email | `admin@example.com` |
| `paperless_ocr_language` | Default OCR language | `eng` |
| `paperless_time_zone` | Time zone for the application | `UTC` |

## Dependencies

- Requires Docker to be installed (recommend using the `install-docker` role first)

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  vars:
    paperless_data_dir: "/data/paperless/data"
    paperless_media_dir: "/data/paperless/media"
    paperless_port: 8123
    paperless_admin_user: "paperless"
    paperless_admin_password: "securepassword"
    paperless_admin_email: "admin@yourdomain.com"
    paperless_ocr_language: "eng+fra" # English and French
  roles:
    - role: install-docker
    - role: app-paperless-ngx
```

## Installation Process

The role performs the following:

1. Creates the necessary directories for Paperless-ngx data
2. Sets up a Docker Compose configuration for Paperless-ngx
3. Deploys the Paperless-ngx containers
4. Configures the initial admin user
5. Sets up the web interface

## Features

- Document scanning and OCR processing
- Full-text search of documents
- Automatic tagging and categorization
- Document type recognition
- Metadata extraction (dates, correspondents, etc.)
- Mobile-friendly web interface
- REST API for integration with other systems
- Multi-user support with permissions

## Security Considerations

- The admin password should be changed from the default
- Consider using HTTPS with a reverse proxy for production deployments
- Backup the data directory regularly to prevent document loss

## License

MIT

## Author Information

Created by WFHT
