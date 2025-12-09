# Set Timezone Role

This role sets the system timezone on Linux systems.

## Requirements

- `community.general` collection (for the `timezone` module)
- Target system must be a supported Linux distribution

## Role Variables

| Variable   | Default | Description                                      |
|------------|---------|--------------------------------------------------|
| `timezone` | `UTC`   | The timezone to set (e.g., `America/New_York`)   |

### Common Timezone Examples

- `UTC` - Coordinated Universal Time
- `America/New_York` - Eastern Time (US)
- `America/Los_Angeles` - Pacific Time (US)
- `Europe/London` - British Time
- `Europe/Paris` - Central European Time
- `Asia/Tokyo` - Japan Standard Time
- `Asia/Tehran` - Iran Standard Time
- `Australia/Sydney` - Australian Eastern Time

You can find a full list of timezones by running `timedatectl list-timezones` on a Linux system.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: omid_fallah_karimi.devops_toolkit.set_timezone
      vars:
        timezone: "Europe/London"
```

## License

GPL-2.0-or-later

## Author Information

Omid Fallah Karimi
