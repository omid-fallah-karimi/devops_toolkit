# Ansible Collection - omid_fallah_karimi.devops_toolkit

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/omid-fallah-karimi/devops_toolkit)
[![License](https://img.shields.io/badge/License-GPL--2.0--or--later-green)](LICENSE)

A collection of Ansible roles for DevOps automation including timezone configuration, package management, repository setup, and Docker installation.

## Requirements

- Ansible >= 2.9
- `community.general` collection

## Installation

### Install from GitHub

```bash
ansible-galaxy collection install git+https://github.com/omid-fallah-karimi/devops_toolkit.git
```

### Install from source

```bash
git clone https://github.com/omid-fallah-karimi/devops_toolkit.git
cd devops_toolkit
ansible-galaxy collection build
ansible-galaxy collection install omid_fallah_karimi-devops_toolkit-1.0.1.tar.gz
```

### Install dependencies

```bash
ansible-galaxy collection install community.general
```

## Included Roles

| Role | Description |
|------|-------------|
| `set_timezone` | Set system timezone on Linux systems |
| `install_packages` | Install packages on Linux (multi-distro support) |
| `add_repository` | Add package repositories on Linux systems |
| `install_docker` | Install Docker CE with optional Compose |

## Supported Platforms

- Debian / Ubuntu
- RedHat / CentOS / Fedora
- Archlinux
- Alpine
- openSUSE

## Usage

### Set Timezone

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.set_timezone
      vars:
        timezone: "Asia/Tehran"
```

### Install Packages

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_packages
      vars:
        packages:
          - vim
          - git
          - curl
          - htop
        package_state: present
```

### Add Repository

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        apt_repositories:
          - repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable"
            key_url: "https://download.docker.com/linux/ubuntu/gpg"
            filename: "docker-ce"
```

### Install Docker

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_docker
      vars:
        docker_users:
          - ubuntu
        docker_install_compose: true
```

### Complete Server Setup

```yaml
- hosts: servers
  become: true
  vars:
    timezone: "UTC"
    packages:
      - vim
      - git
      - curl

  roles:
    - role: omid_fallah_karimi.devops_toolkit.set_timezone
    - role: omid_fallah_karimi.devops_toolkit.install_packages
    - role: omid_fallah_karimi.devops_toolkit.install_docker
      vars:
        docker_users:
          - ubuntu
```

## Example Project

See `docs/example-project/` for a complete example with best practices:
- Separate inventory per environment (staging/production)
- Group variables
- Ready-to-use playbooks

## License

GPL-2.0-or-later

## Author

Omid Fallah Karimi

- GitHub: [@omid-fallah-karimi](https://github.com/omid-fallah-karimi)
- Email: omid.fallah.karimi@gmail.com
