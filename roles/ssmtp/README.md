# SSMTP Role

Installs and configures ssmtp for sending email notifications via external SMTP server.

## Configuration

- Mail relay: `smtp.fastmail.com:587`
- STARTTLS enabled
- Uses vault-encrypted credentials from `group_vars/all.yml`:
  - `my_email` - Authentication username and sender address
  - `smtp_password` - Authentication password
  - `my_domain` - Rewrite domain

## Templates

- `ssmtp.conf.j2` - ssmtp configuration file

## Dependencies

Variables from `group_vars/all.yml`
