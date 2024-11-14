---
id: flatpak
aliases: []
tags: []
---

# Flatpak

Flatpak is a system for distributing and installing desktop applications on Linux. It is a modern build of the traditional .deb packager for Linux.

[Website](https://flatpak.org/)

## Installation

### Ubuntu

> Reference: [Ubuntu Quick Setup](https://flatpak.org/setup/Ubuntu)

```bash
sudo apt install flatpak
```

#### Flathub

Flathub is the best place to get Flatpak apps. To enable it, run the following command:

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

## Usage

### Install

Install a Flatpak app.

```bash
flatpak install <app>
```

### List

List installed Flatpak apps.

```bash
flatpak list
```

### Remove

Remove a Flatpak app.

```bash
flatpak remove <app>
```

### Run

Run a Flatpak app.

```bash
flatpak run <app>
```

### Update

Update a Flatpak app.
With no argument, updates all installed Flatpak apps.

```bash
flatpak update <app>
```
