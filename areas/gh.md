---
id: gh
aliases:
  - githbub-cli
tags:
  - github
  - cli
  - terminal
---

# GitHub CLI

GitHub CLI brings GitHub to your terminal. Free and open source.

[Website](https://cli.github.com/)

## Installation

### macOS

> Reference: [macOS](https://github.com/cli/cli?tab=readme-ov-file#macos)

```bash
brew install gh
```

### Linux

> Reference: [Debian, Ubuntu Linux, Raspberry Pi OS (apt)](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#debian-ubuntu-linux-raspberry-pi-os-apt)

```bash
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
	&& wget -qO- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& sudo apt update \
	&& sudo apt install gh -y
```

## Configuration

### Editor

```bash
gh config set editor nvim
```

## Usage

### Authentication

Authenticate with a GitHub host.
The default hostname is `github.com`. This can be overridden using the `--hostname` flag.

```bash
gh auth login
```

### Clone

Clone a GitHub repository locally. Pass additional `git clone` flags by listing them after `--`.
If the `<owner>/` portion of the `<owner>/<repo>` repository argument is omitted, it defaults to the name of the authenticating user.

```bash
gh repo clone <owner>/<repo>
```

### Create

Create a new GitHub repository.
To create a repository interactively, use `gh repo create` with no arguments.

```bash
gh repo create <owner>/<repo>
```

### Delete

Delete a GitHub repository.
With no argument, deletes the current repository. Otherwise, deletes the specified repository.

```bash
gh repo delete <owner>/<repo>
```

### List

List repositories owned by a user or organization.

```bash
gh repo list
```

### View

Display the description and the `README` of a GitHub repository.
With no argument, the repository for the current directory is displayed.

```bash
gh repo view <owner>/<repo>
```
