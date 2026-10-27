# Dotfiles

My tmux, herdr, Neovim, and zsh configuration, captured from my Linux/WSL machine on 2026-10-27.

## Contents

- `zsh/.zshrc`: Oh My Zsh with the `robbyrussell` theme and `git` plugin, Go and local Node paths, nvm, Fly CLI, and CopyQ startup. The original absolute home-directory paths use `$HOME` here.

- `tmux/.tmux.conf`: locally modified Oh my tmux! configuration, including the `Ctrl+q` prefix, `Alt+h`/`Alt+l` window navigation, vi copy mode, and a shorter repeat timeout. `Ctrl+a` remains an alternate prefix.
- `tmux/.tmux.conf.local`: zsh, true-color settings, `R` for rectangular selection in vi copy mode, and the `hiroppy/tmux-agent-sidebar` plugin.
- `herdr/config.toml`: `Ctrl+q` prefix, vim-style pane navigation, `Alt+h`/`Alt+l` tab navigation, blue accent, and a clipboard cleanup command on prefix + `Shift+y`.
- `nvim/`: customized Kickstart configuration with Space as leader, Telescope, Go LSP (`gopls`), Go formatting on save, Blink completion, Treesitter, and the Tokyo Night theme. Includes the plugin lockfile.

This is a configuration snapshot. Binaries, downloaded plugins, logs, session state, credentials, shell history, and source repository histories are excluded.

## Requirements

The source machine has tmux 3.6a, herdr 0.7.5, and Neovim 0.12.2. Other versions have not been verified.

Both multiplexers expect zsh at `/usr/bin/zsh`. Adjust the shell setting if yours is elsewhere. Neovim uses Git, Make, a C compiler, unzip, and ripgrep; Go development also needs Go and `gofmt`. The herdr clipboard command needs `xclip` and access to an X11 clipboard. Neovim clipboard support needs a working clipboard provider.

## Zsh dependencies

The source machine uses zsh 5.9. Install Oh My Zsh at `~/.oh-my-zsh` before loading this configuration; its bundled `robbyrussell` theme and `git` plugin are sufficient. No custom plugins or themes are enabled.

The configuration also adds paths for Go (`/usr/local/go` and `~/go/bin`), local Node (`~/.local/node/bin`), and Fly CLI (`~/.fly/bin`). It loads nvm from `~/.nvm` when installed and starts CopyQ on every interactive shell. Install those tools as needed, or adjust their sections for your machine.

## Install

Install the applications and dependencies first, then clone:

```sh
git clone https://github.com/bearjah/dotfiles.git "$HOME/dotfiles"
cd "$HOME/dotfiles"
```

Back up any existing `~/.zshrc`, `~/.tmux.conf`, `~/.tmux.conf.local`, `~/.config/herdr/config.toml`, and `~/.config/nvim` before proceeding. The commands below overwrite files with matching names; use a fresh Neovim configuration directory to avoid mixing configurations.

```sh
mkdir -p "$HOME/.config/herdr" "$HOME/.config/nvim"
cp zsh/.zshrc "$HOME/.zshrc"
cp tmux/.tmux.conf "$HOME/.tmux.conf"
cp tmux/.tmux.conf.local "$HOME/.tmux.conf.local"
cp herdr/config.toml "$HOME/.config/herdr/config.toml"
cp -R nvim/. "$HOME/.config/nvim/"
```

The install commands copy the configurations so the checkout can be moved or removed afterward.

Start a new tmux session to load the configuration; Oh my tmux! can install TPM and the configured sidebar plugin on launch. For an existing server, reload with `tmux source-file "$HOME/.tmux.conf"`.

Start a new zsh shell to load `.zshrc`.

Start herdr to load its configuration. Open Neovim to bootstrap lazy.nvim, then run `:Lazy restore` to restore the plugin revisions in `lazy-lock.json`. Mason and Treesitter can download language tools and parsers. Run `:checkhealth` to inspect missing dependencies. See [the upstream Kickstart guide](nvim/README.upstream.md) for configuration details.

## Upstream sources and licenses

- tmux is based on [gpakosz/.tmux](https://github.com/gpakosz/.tmux), local base commit `af33f07134b76134acca9d01eacbdecca9c9cda6`, with the modifications described above. Its MIT and WTFPL v2 licenses are preserved in `tmux/`.
- Neovim is based on [nvim-lua/kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim), local base commit `4b065ad`, with local configuration changes. Its MIT license is preserved in `nvim/LICENSE.md`.
