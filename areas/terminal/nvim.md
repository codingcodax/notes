---
id: nvim
aliases: []
tags: []
---

# Neovim

Hyperextensible Vim-based text editor.

> [Website](https://neovim.io/)

## Installation

### macOS

> Reference: [Homebrew on macOS or Linux](https://github.com/neovim/neovim/blob/master/INSTALL.md#homebrew-on-macos-or-linux)

```bash
brew install neovim
```

### Linux

> Reference: [Linux](https://github.com/neovim/neovim/blob/master/INSTALL.md#appimage-universal-linux-package)

```bash
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```

To expose `nvim` globally:

```bash
mkdir -p /opt/nvim
mv nvim.appimage /opt/nvim/nvim
```
