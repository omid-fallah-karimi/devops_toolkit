# Ansible Collection - omid_fallah_karimi.devops_toolkit

[![GitHub](https://img.shields.io/badge/GitHub-Repository-blue)](https://github.com/omid-fallah-karimi/devops_toolkit)
[![License](https://img.shields.io/badge/License-GPL--2.0--or--later-green)](LICENSE)

A collection of Ansible roles for DevOps automation including timezone configuration, package management, and repository setup.

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
ansible-galaxy collection install omid_fallah_karimi-devops_toolkit-1.0.0.tar.gz
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
    apt_repositories:
      - repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable"
        key_url: "https://download.docker.com/linux/ubuntu/gpg"
        filename: "docker-ce"

  roles:
    - role: omid_fallah_karimi.devops_toolkit.set_timezone
    - role: omid_fallah_karimi.devops_toolkit.add_repository
    - role: omid_fallah_karimi.devops_toolkit.install_packages
```

## Playbooks

The collection includes ready-to-use playbooks:

- `playbooks/setup_server.yml` - Complete server setup with timezone and packages

```bash
ansible-playbook -i inventory omid_fallah_karimi.devops_toolkit.setup_server \
  -e "timezone=Asia/Tehran"
```

## License

GPL-2.0-or-later

## Author

Omid Fallah Karimi

- GitHub: [@omid-fallah-karimi](https://github.com/omid-fallah-karimi)
- Email: omid.fallah.karimi@gmail.com
