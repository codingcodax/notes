---
id: lazygit
aliases: []
tags:
  - macOS
  - linux
  - terminal
---

# LazyGit

Simple terminal UI for git commands.

> [GitHub Repository](https://github.com/jesseduffield/lazygit)

## Installation

### macOS

> Reference: [Homebrew](https://github.com/jesseduffield/lazygit?tab=readme-ov-file#homebrew)

```bash
brew install jesseduffield/lazygit/lazygit
```

### Ubuntu

> Reference: [Ubuntu](https://github.com/jesseduffield/lazygit?tab=readme-ov-file#ubuntu)

```bash
LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | \grep -Po '"tag_name": *"v\K[^"]*')
curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/download/v${LAZYGIT_VERSION}/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
tar xf lazygit.tar.gz lazygit
sudo install lazygit -D -t /usr/local/bin/
```
