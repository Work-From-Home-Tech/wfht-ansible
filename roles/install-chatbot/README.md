# Ansible Role: install-chatbot

This Ansible role installs and configures a self-hosted chatbot solution, providing an AI-powered conversational interface that can be integrated with various platforms and services.

## Requirements

- Ansible 2.1 or higher
- Docker and Docker Compose (recommended for deployment)
- Minimum 4GB RAM on target system
- 10GB+ free disk space

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `chatbot_install_dir` | Installation directory | `/opt/chatbot` |
| `chatbot_model` | AI model to use | `gpt-3.5-turbo` |
| `chatbot_api_key` | API key for the AI service | Required, no default |
| `chatbot_port` | Port for the web interface | `3000` |
| `chatbot_memory_limit` | Memory limit for the container | `4g` |
| `chatbot_enable_web_ui` | Enable web interface | `true` |
| `chatbot_enable_api` | Enable API access | `true` |
| `chatbot_log_level` | Logging level | `info` |
| `chatbot_admin_user` | Admin username | `admin` |
| `chatbot_admin_password` | Admin password | Generated randomly |

## Dependencies

- Requires Docker to be installed (recommend using the `install-docker` role first)

## Example Playbook

Basic usage:
```yaml
- hosts: servers
  become: true
  vars:
    chatbot_api_key: "your-api-key-here"
  roles:
    - role: install-docker
    - role: install-chatbot
```

Advanced configuration:
```yaml
- hosts: servers
  become: true
  vars:
    chatbot_api_key: "your-api-key-here"
    chatbot_model: "gpt-4"
    chatbot_install_dir: "/data/chatbot"
    chatbot_port: 8080
    chatbot_memory_limit: "8g"
    chatbot_admin_user: "chatbot_admin"
    chatbot_admin_password: "secure_password"
  roles:
    - role: install-docker
    - role: install-chatbot
```

## Installation Process

The role performs the following:

1. Creates the necessary directories for the chatbot
2. Sets up configuration files with the specified parameters
3. Deploys the chatbot using Docker Compose
4. Configures the web interface and API
5. Sets up the admin user

## Features

- Natural language processing capabilities
- Web-based chat interface
- REST API for integration with other systems
- Customizable responses and behaviors
- Support for multiple AI models
- Conversation history and context management
- User authentication and access control
- Extensible plugin system

## Integration Options

The chatbot can be integrated with:
- Slack
- Discord
- Microsoft Teams
- Telegram
- Custom web applications
- Mobile apps via the API

## Security Considerations

- Store API keys securely
- Use strong admin passwords
- Enable HTTPS for production deployments
- Implement proper access controls
- Regularly update the chatbot software

## License

MIT

## Author Information

Created by WFHT
