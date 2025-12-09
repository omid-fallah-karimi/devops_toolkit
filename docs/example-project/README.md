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
    ├── bootstrap.yml        # Initial server setup
    ├── setup_repos.yml      # Configure repositories
    └── site.yml             # Main playbook
```

## Usage

1. Install the collection:
   ```bash
   ansible-galaxy collection install -r requirements.yml
   ```

2. Run a playbook:
   ```bash
   # Staging
   ansible-playbook -i inventory/staging/hosts playbooks/bootstrap.yml

   # Production
   ansible-playbook -i inventory/production/hosts playbooks/bootstrap.yml
   ```
