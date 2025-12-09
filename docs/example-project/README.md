# Example Infrastructure Project

This directory contains an example of how to use the `omid_fallah_karimi.devops_toolkit` collection in a real project.

## Structure

```
my-infrastructure/
├── ansible.cfg              # Ansible configuration
├── requirements.yml         # Collection dependencies
├── inventory/
│   ├── production/
│   │   ├── hosts            # Production inventory
│   │   └── group_vars/
│   │       ├── all.yml      # Variables for all hosts
│   │       └── webservers.yml
│   └── staging/
│       ├── hosts            # Staging inventory
│       └── group_vars/
│           └── all.yml
└── playbooks/
    ├── bootstrap.yml        # Initial server setup (timezone, packages, optional Docker)
    ├── setup_repos.yml      # Configure repositories
    └── site.yml             # Complete setup with Docker
```

## Available Roles

| Role | Description |
|------|-------------|
| `set_timezone` | Set system timezone |
| `install_packages` | Install packages (multi-distro) |
| `add_repository` | Add package repositories |
| `install_docker` | Install Docker CE with Compose |

## Usage

1. Install the collection:
   ```bash
   ansible-galaxy collection install -r requirements.yml
   ```

2. Run a playbook:
   ```bash
   # Bootstrap (timezone + packages)
   ansible-playbook -i inventory/staging/hosts playbooks/bootstrap.yml

   # Complete setup with Docker
   ansible-playbook -i inventory/production/hosts playbooks/site.yml
   ```

3. Override variables:
   ```bash
   ansible-playbook -i inventory/staging/hosts playbooks/site.yml \
     -e "timezone=Europe/London" \
     -e "install_docker=true"
   ```

## Key Variables

Configure these in `group_vars/all.yml`:

| Variable | Default | Description |
|----------|---------|-------------|
| `timezone` | `UTC` | System timezone |
| `base_packages` | `[vim, curl, ...]` | Packages to install |
| `install_docker` | `true` | Install Docker |
| `docker_users` | `[ubuntu]` | Users to add to docker group |
| `docker_install_compose` | `true` | Install Docker Compose |
