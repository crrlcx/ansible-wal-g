# About

Ansible role `ansible-wal-g` installs wal-g binary from github releases.

## Requirements

- systemd

## Role variables

```yaml
# wal-g version to fetch
walg_version: 0.2.15

# default wal-g releases repository url
walg_url: "https://github.com/wal-g/wal-g/releases/download/v{{ walg_version }}/wal-g.linux-amd64.tar.gz"

# wal-g install path
walg_binary_path: /usr/local/bin
```

## Dependencies

-

## Example playbook

```yaml
- hosts: servers
  roles:
    - role: ansible-wal-g
      walg_version: 0.2.15
```

## License

MIT
