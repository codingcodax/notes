---
id: astronvim
aliases: []
tags:
  - nvim
  - terminal
---

# AstroNvim

Aesthetically pleasing and feature-rich Neovim configuration that focuses on extensibility and usability.

> [Website](https://astronvim.com/)

## Requirements

> Reference: [Requirements](https://astronvim.com/#-requirements)

- [Nerd Fonts](https://www.nerdfonts.com/) -> [Maple Mono NF](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/MapleMono)
- [[nvim|neovim]]
- [Tree-sitter CLI](https://github.com/tree-sitter/tree-sitter/blob/master/cli/README.md#installation)
- [[ripgrep]]
- [[lazygit]]
- [[bottom]]

## Installation

> Reference: [Installation](https://astronvim.com/#-installation)

1. Make a backup of your current nvim config (if exists)

   ```bash
   mv ~/.config/nvim ~/.config/nvim.bak
   ```

2. Clean neovim folders (Optional but recommended)

   ```bash
   mv ~/.local/share/nvim ~/.local/share/nvim.bak
   mv ~/.local/state/nvim ~/.local/state/nvim.bak
   mv ~/.cache/nvim ~/.cache/nvim.bak
   ```

3. Clone the repository

   ```bash
   gh repo clone AstroNvim/template -- --depth 1 ~/.config/nvim
   rm -rf ~/.config/nvim/.git
   nvim
   ```

## Setup

> Reference: [Setup](https://astronvim.com/#-setup)

- Update Mason packages and plugins
  Run `:AstroUpdate` (`<Leader>pa`) to update both Neovim plugins and Mason packages.

- Manage plugins

  - Run `:Lazy check` (`<Leader>pu`) to check for plugin updates.
  - Run `:Lazy update` (`<Leader>pU`) to apply any pending plugin updates.
  - Run `:Lazy sync` (`<Leader>pS`) to update and clean plugins.
  - Run `:Lazy clean` to remove any disabled or unused plugins.

- Install LSP
  Enter `:LspInstall` followed by the name of the server you want to install.

  > [!EXAMPLE]
  > Install `pyright` -> `:LspInstall pyright`

- Install language parser
  Enter `:TSInstall` followed by the name of the language you want to install.

  > [!EXAMPLE]
  > Install `python` -> `:TSInstall python`

- Install Debugger
  Enter `:DapInstall` followed by the name of the debugger you want to install.

  > [!EXAMPLE]
  > Install for `python` -> `:DapInstall python`

- Check AstroNvim version
  Run `:AstroVersion` to display the currently installed AstroNvim version.

- Reload AstroNvim (EXPERIMENTAL)
  Run `:AstroReload` to reload the AstroNvim configuration and any new user configuration changes without restarting.
  This is currently an experimental feature and may lead to instability until the next restart.

# Features

- Common plugin specifications with [AstroCommunity](https://github.com/AstroNvim/astrocommunity)
- Statusline, Winbar, and Tabline with [Heirline](https://github.com/rebelot/heirline.nvim)
- Plugin management with [`lazy.nvim`](https://github.com/folke/lazy.nvim)
- Package management with [`mason.nvim`](https://github.com/williamboman/mason.nvim)
- File explorer with [Neo-tree](https://github.com/nvim-neo-tree/neo-tree.nvim)
- Autocompletion with [Cmp](https://github.com/hrsh7th/nvim-cmp)
- Syntax highlighting with [Treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
- Formatting and linting with [`none-ls`](https://github.com/nvimtools/none-ls.nvim)
- Language Server Protocol with [Native LSP](https://github.com/neovim/nvim-lspconfig)
