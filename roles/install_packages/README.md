# Install Packages Role

This role installs packages on Linux systems with support for multiple distributions.

## Requirements

- `community.general` collection (for pacman, apk, and zypper modules)
- Target system must be a supported Linux distribution

## Supported Distributions

- Debian / Ubuntu (apt)
- RedHat / CentOS / Fedora (yum/dnf)
- Archlinux (pacman)
- Alpine (apk)
- openSUSE (zypper)

## Role Variables

| Variable           | Default   | Description                                      |
|--------------------|-----------|--------------------------------------------------|
| `packages`         | `[]`      | List of packages to install                      |
| `package_state`    | `present` | Package state: `present`, `latest`, or `absent`  |
| `cache_valid_time` | `3600`    | Cache validity in seconds (apt only)             |
| `update_cache`     | `true`    | Update package cache before installing           |

## Dependencies

None.

## Example Playbook

### Install specific packages

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
```

### Install and ensure latest version

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_packages
      vars:
        packages:
          - nginx
          - docker
        package_state: latest
```

### Remove packages

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.install_packages
      vars:
        packages:
          - apache2
          - httpd
        package_state: absent
```

## License

GPL-2.0-or-later

## Author Information

Omid Fallah Karimi
