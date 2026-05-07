# Common Role

Updates package cache, upgrades system packages, and installs essential tools for all nodes.

## Packages Installed

- apt-transport-https, ca-certificates
- restic, tmux, jq, gnupg, lsb-release
- zsh, starship, curl, git, vim
- htop, sudo, net-tools, mc, cron

## Configuration

- Sets timezone to `Europe/Amsterdam`
- Adds git aliases: `st` (status), `core.editor` (vim)
- Deploys midnight commander (`mc`) configuration to `~/.config/mc/ini` with sensible defaults

## Dependencies

None
