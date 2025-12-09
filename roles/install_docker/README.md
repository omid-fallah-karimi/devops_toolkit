# Install Docker Role

This role installs Docker CE on Linux systems.

## Requirements

- Supported Linux distribution (Debian, Ubuntu, CentOS, RHEL, Fedora)
- Internet access to download Docker packages

## Supported Platforms

- Debian 11 (Bullseye), 12 (Bookworm)
- Ubuntu 20.04 (Focal), 22.04 (Jammy), 24.04 (Noble)
- CentOS/RHEL 8, 9
- Fedora (latest versions)

## Role Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `docker_remove_old` | `true` | Remove old Docker versions |
| `docker_packages` | `[docker-ce, docker-ce-cli, ...]` | Docker packages to install |
| `docker_service_enabled` | `true` | Enable Docker service on boot |
| `docker_service_state` | `started` | Docker service state |
| `docker_users` | `[]` | Users to add to docker group |
| `docker_install_compose` | `false` | Install Docker Compose standalone |
| `docker_compose_version` | `latest` | Docker Compose version |
| `docker_daemon_config` | `{}` | Docker daemon configuration |

## Dependencies

None.

## Example Playbook

### Basic Installation

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_docker
```

### With User Access

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_docker
      vars:
        docker_users:
          - ubuntu
          - deploy
```

### With Docker Compose and Custom Config

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_docker
      vars:
        docker_install_compose: true
        docker_users:
          - ubuntu
        docker_daemon_config:
          storage-driver: overlay2
          log-driver: json-file
          log-opts:
            max-size: "10m"
            max-file: "3"
```

### Full Example with All Roles

```yaml
- hosts: servers
  become: true
  vars:
    timezone: "UTC"
    base_packages:
      - vim
      - git
      - curl

  roles:
    - role: omid_fallah_karimi.devops_toolkit.set_timezone
    - role: omid_fallah_karimi.devops_toolkit.install_packages
      vars:
        packages: "{{ base_packages }}"
    - role: omid_fallah_karimi.devops_toolkit.install_docker
      vars:
        docker_users:
          - ubuntu
```

## License

GPL-2.0-or-later

## Author Information

Omid Fallah Karimi
