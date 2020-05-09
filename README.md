# About

Ansible role `ansible-wal-g` installs wal-g binary from github releases.

## Requirements

- cron | systemd-cron

## Role variables

```yaml
# wal-g version to fetch
walg_version: 0.2.15

# wal-g releases repository url
walg_url: "https://github.com/wal-g/wal-g/releases/download/v{{ walg_version }}/wal-g.linux-amd64.tar.gz"

# wal-g binary place
walg_binary: /usr/local/bin/wal-g

# wal-g setting place
walg_env: /etc/default/wal-g

# wal-g scripts place
walg_script_path: /usr/local/scripts

# S3 bucket settings
walg_s3_access_key: "access"
walg_s3_bucket: "wal-g"
walg_s3_prefix: "backup"
walg_s3_region: us-west-1
walg_s3_secret_access_key: "secret"

# How many full backups should stay after rotation
walg_backups_retain: 7

# Create cron jobs
walg_cron_enabled: true
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

## PostgreSQL settings

- `archive_command = '/usr/local/scripts/walg-push.sh %p &> /dev/null'`
- `restore_command = '/usr/local/scripts/walg-fetch.sh "%f" "%p"'`

## Usage

Create full or delta backups with: `/usr/local/scripts/walg-backup.sh`\
Rotate WAL-archives and backups with: `/usr/local/scripts/walg-rotate.sh`

## License

MIT
