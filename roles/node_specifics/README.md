# Node Specifics Role

Handles node-specific configuration including cron jobs, NFS setup, and Docker installation.

## Tasks

### Common (All Nodes)

- Configures cron email notifications (root and rlommers user)

### services Node

- Installs Docker and Docker Compose
- Creates `/srv/local` directory
- Sets up cron jobs:
  - Daily backup to Hetzner at 03:30
  - Hourly XML feed generation at :15
- Installs NFS client packages
- Mounts NFS share from `nas-nijmegen` at `/srv/nas`

### nas-nijmegen Node

- Creates `/srv/local` and `/srv/nas` directories
- Installs and configures NFS server
- Sets up cron jobs:
  - Daily scheduled file deletions at 00:00
  - Weekly Hetzner backup prune/check on Sundays at 06:00

## Variables

- `hc_backup_hetzner_uuid` - Healthchecks UUID for backup ping
- `hc_xml_feed_uuid` - Healthchecks UUID for XML feed ping
- `hc_purge_hetzner_uuid` - Healthchecks UUID for prune/check ping
- `my_email` - Email address for notifications

## Dependencies

- `roles/common` (for restic installation on NAS node)
- `roles/ssh` (for scripts directory access)
