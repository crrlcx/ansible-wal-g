# About

Ansible role `ansible-wal-g` installs **[wal-g](https://github.com/wal-g/wal-g)** binary from github [releases](https://github.com/wal-g/wal-g/releases).

WAL-G is an archival restoration tool for Postgres (beta for MySQL, MongoDB, and Redis)

WAL-G is the successor of WAL-E with a number of key differences. WAL-G uses LZ4, LZMA, or Brotli compression,\
multiple processors, and non-exclusive base backups for Postgres.\

## Requirements

- cron | systemd-cron

## Role variables

### Defaults

```yaml
# wal-g version to fetch
walg_version: 0.2.15

# wal-g releases repository url
walg_url: "https://github.com/wal-g/wal-g/releases/download/v{{ walg_version }}/wal-g.linux-amd64.tar.gz"

# wal-g download checksum (get it from the release page or directly from : "{{ walg_url }}.sha256")
walg_sha256_checksum:

# wal-g binary place
walg_binary: /usr/local/bin/wal-g

# user for cronjob
walg_user: postgres

# wal-g setting place
walg_env: /etc/default/wal-g

# wal-g scripts place
walg_script_path: /usr/local/scripts

# S3 bucket required settings
walg_s3_id: "access"
walg_s3_secret: "secret"
walg_s3_bucket: backup
walg_s3_prefix: db

# S3 bucket optional settings
walg_s3_storage_class: STANDARD | STANDARD_IA | REDUCED_REDUNDANCY
walg_s3_use_path_style: false | true
walg_s3_region: us-west-1
walg_s3_endpoint: "https://s3.dualstack.{{ walg_s3_region }}.amazonaws.com"

# Disk usage
walg_backup_upload_disk: 2

# Network usage
walg_backup_upload: 10
walg_backup_download: 10

# How many delta backups should stay between full backups
walg_backup_delta_steps: 7

# How many full backups should stay after rotation
walg_backups_retain: 2

# Create cron jobs
walg_cron_enabled: true
```

### Override

All variables from this groups will be combined with same `_config` groups in `vars/main.yml`.

```yaml
# Override WAL-G settings
## Storages
walg_aws_override: []
walg_azure_override: []
walg_gcs_override: []
walg_swift_override: []
walg_filesystem_override: []

## Databases
walg_mongodb_override: []
walg_mysql_override: []
walg_postgresql_override: []

## Commons
walg_common_override: []
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

## Support author

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.digitaloceanspaces.com/WWW/Badge%202.svg)](https://www.digitalocean.com/?refcode=53db0fdc3ada&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)You can support me with DO ref program
