# QEMU Guest Role

Installs and configures the QEMU guest agent for Proxmox VM communication.

## Tasks

- Installs `qemu-guest-agent` package
- Enables and starts `qemu-guest-agent.service`

## Notes

- VM may need cold reboot (not just OS restart) for QEMU agent to function properly
- Used for Proxmox VM communication and live migrations

## Dependencies

None
