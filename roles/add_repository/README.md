# Add Repository Role

This role adds package repositories on Linux systems with support for multiple distributions.

## Requirements

- `community.general` collection (for zypper and pacman modules)
- Target system must be a supported Linux distribution

## Supported Distributions

- Debian / Ubuntu (apt)
- RedHat / CentOS / Fedora (yum/dnf)
- Archlinux (pacman)
- Alpine (apk)
- openSUSE (zypper)

## Role Variables

### Global Options

| Variable              | Default | Description                                      |
|-----------------------|---------|--------------------------------------------------|
| `skip_gpg_check`      | `false` | Skip GPG key verification (use with caution!)    |
| `purge_existing_repos`| `false` | Remove all existing repositories before adding   |

### APT Repositories (Debian/Ubuntu)

| Variable          | Default | Description                    |
|-------------------|---------|--------------------------------|
| `apt_repositories`| `[]`    | List of APT repositories       |

Each APT repository can have:
- `repo` (required): Repository line
- `key_url`: URL to GPG key
- `keyserver`: Keyserver URL
- `key_id`: GPG key ID
- `filename`: Repository filename

### YUM/DNF Repositories (RedHat/CentOS/Fedora)

| Variable          | Default | Description                    |
|-------------------|---------|--------------------------------|
| `yum_repositories`| `[]`    | List of YUM repositories       |

Each YUM repository can have:
- `name` (required): Repository name
- `description`: Repository description
- `baseurl`: Base URL
- `mirrorlist`: Mirror list URL
- `gpgkey`: GPG key URL
- `gpgcheck`: Enable GPG check (default: true)
- `enabled`: Enable repository (default: true)

### Zypper Repositories (SUSE)

| Variable            | Default | Description                  |
|---------------------|---------|------------------------------|
| `zypper_repositories`| `[]`   | List of Zypper repositories  |

### Alpine Repositories

| Variable             | Default | Description                 |
|----------------------|---------|-----------------------------|
| `alpine_repositories`| `[]`   | List of Alpine repositories |

### Pacman Repositories (Archlinux)

| Variable             | Default | Description                 |
|----------------------|---------|-----------------------------|
| `pacman_repositories`| `[]`   | List of Pacman repositories |

## Dependencies

None.

## Example Playbook

### Add Docker repository on Ubuntu

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

### Add EPEL repository on CentOS

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        yum_repositories:
          - name: "epel"
            description: "Extra Packages for Enterprise Linux"
            baseurl: "https://dl.fedoraproject.org/pub/epel/$releasever/$basearch/"
            gpgkey: "https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-$releasever"
            gpgcheck: true
```

### Add multiple repositories

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        apt_repositories:
          - repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable"
            key_url: "https://download.docker.com/linux/ubuntu/gpg"
            filename: "docker-ce"
          - repo: "deb https://packages.grafana.com/oss/deb stable main"
            key_url: "https://packages.grafana.com/gpg.key"
            filename: "grafana"
```

### Skip GPG key verification

⚠️ **Warning**: Only use this option in trusted environments or for testing purposes.

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        skip_gpg_check: true
        apt_repositories:
          - repo: "deb http://internal-mirror.example.com/ubuntu focal main"
            filename: "internal-mirror"
```

### Purge existing repositories and add new ones

This will remove all existing repository configurations before adding the new ones.

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        purge_existing_repos: true
        apt_repositories:
          - repo: "deb http://archive.ubuntu.com/ubuntu focal main restricted"
            filename: "ubuntu-main"
          - repo: "deb http://archive.ubuntu.com/ubuntu focal-updates main restricted"
            filename: "ubuntu-updates"
```

### Purge repos and skip GPG (fresh VM setup)

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.add_repository
      vars:
        purge_existing_repos: true
        skip_gpg_check: true
        yum_repositories:
          - name: "custom-repo"
            description: "Custom Internal Repository"
            baseurl: "http://internal-repo.example.com/centos/$releasever/$basearch/"
```

## License

GPL-2.0-or-later

## Author Information

Omid Fallah Karimi
