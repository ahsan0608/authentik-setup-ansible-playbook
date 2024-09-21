# Authentik Ansible Playbook

## Overview

This playbook installs all necessary dependencies, configures environment variables, and starts Authentik services, making the setup process seamless.

## Project Structure

```plaintext
authentik-setup/
├── ansible.cfg
├── inventory
│   └── hosts
├── playbooks
│   └── setup_authentik.yml
└── roles
    └── authentik
        ├── tasks
        │   └── main.yml
        ├── templates
        │   ├── docker-compose.yml.j2
        │   └── .env.j2
        └── vars
            └── main.yml
```

## Configuration

### 1. Inventory

Update the `inventory/hosts` file with the IP address of your remote VM. Replace `your_vm_ip` with the actual IP:

```ini
[authentik]
your_vm_ip

[authentik:vars]
ansible_python_interpreter=/usr/bin/python3
```

### 2. Variables

Set the required variables in `roles/authentik/vars/main.yml`:

```yaml
postgres_password: "your_secure_password"
postgres_user: "authentik"
postgres_db: "authentik"
authentik_image: "ghcr.io/goauthentik/server:2023.2.2"
authentik_port_http: 9000
authentik_port_https: 9443
secret_key: "your_generated_secret_key"
```

## Running the Playbook

This command will prompt you for the sudo password to install Docker and Docker Compose on the remote VM:

   ```bash
   ansible-playbook playbooks/setup_authentik.yml
   ```
