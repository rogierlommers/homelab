# SSH Role

Manages SSH configuration and key-based authentication.

## Tasks

- Creates `~/.ssh` directory with correct permissions
- Deploys SSH private/public key pairs (local and Hetzner)
- Generates `~/.ssh/config` with host-specific settings
- Hardens sshd_config:
  - Disables root login
  - Disables password authentication
  - Disables X11 forwarding
  - Disables empty passwords
- Restarts sshd if configuration changed

## Templates

- `id_ed25519.j2` - Primary SSH private key (vault encrypted)
- `id_ed25519.pub.j2` - Primary SSH public key
- `id_ed25519_hetzner.j2` - Hetzner storage box key (vault encrypted)
- `id_ed25519.pub_hetzner.j2` - Hetzner public key
- `ssh_config.j2` - SSH client configuration

## Dependencies

None
