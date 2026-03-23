# Dotfiles Role

Clones and symlinks user dotfiles and configuration files.

## Tasks

- Sets default shell to `/bin/zsh`
- Clones `git@github.com:rogierlommers/dotfiles.git` repository
- Clones antidote plugin manager
- Creates symlinks for:
  - `~/scripts` -> dotfiles scripts
  - `~/.tmux.conf` -> tmux configuration
  - `~/.zshrc` -> zsh configuration
  - `~/.zsh_aliases.sh`, `~/.zsh_functions.sh`, `~/.zsh_plugins.txt`, `~/.zsh_config.sh`
  - `~/.config/starship.toml` -> starship prompt config
  - `~/.ripgrep.conf` -> ripgrep config
- Adds scripts directory to system PATH via `/etc/profile.d/`

## Dependencies

Requires `roles/ssh` to be run first (for SSH hostkey acceptance of GitHub)
