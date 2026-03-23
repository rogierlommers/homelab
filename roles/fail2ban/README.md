# Fail2ban Role

Installs and configures fail2ban to protect against brute-force attacks.

## Configuration

- Ban time: 86400s (24 hours)
- Find time: 120s
- Ignored IPs: 127.0.0.0
- Notifications sent via sendmail to configured email

## Templates

- `customisation.local.j2` - fail2ban jail configuration

## Usage

- Unban IP: `sudo fail2ban-client set sshd unbanip <ip>`
- Check banned clients: `sudo fail2ban-client status sshd`

## Dependencies

None
