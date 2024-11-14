---
id: oh-my-zsh
aliases: []
tags:
  - linux
  - macOS
  - terminal
---

# Oh My Zsh

Framework for managing your zsh configuration.

## Installation

> Reference: [Installing ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

### Zsh

#### macOS

```bash
brew install zsh
```

#### Ubuntu

```bash
sudo apt install zsh
```

#### Arch

```bash
sudo pacman -S zsh
```

### Oh My Zsh

> Reference: [Basic Installation](https://github.com/ohmyzsh/ohmyzsh#basic-installation)

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Oh My Zsh

#### `curl`

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### `wget`

```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Configuration

The configuration file is located at `~/.zshrc`.
We have 3 internal and 3 external plugins. In addition to multiple aliases and functions.
Also we have a custom zsh theme called `kosori` that we will use.

### Plugins

#### `git-trim`

> Reference: [Installing via ZSH](https://github.com/jasonmccreary/git-trim?tab=readme-ov-file#oh-my-zsh)

```bash
git clone https://github.com/jasonmccreary/git-trim.git $ZSH_CUSTOM/plugins/git-trim
```

```bash
gh clone jasonmccreary/git-trim $ZSH_CUSTOM/plugins/git-trim
```

#### `zsh-autosuggestions`

> Reference: [Oh My Zsh](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```bash
gh repo clone zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### `zsh-syntax-highlighting`

> Reference: [Oh My Zsh](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md#oh-my-zsh)

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

```bash
gh repo clone zsh-users/zsh-syntax-highlighting ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Theme

The theme is located at `~/.oh-my-zsh/custom/themes/kosori.zsh-theme`.

```bash
# Promp text information
PROMPT='%B$FG[183] %B$FG[183]%c $(git_prompt_info)%{$reset_color%}$(_git_time_since_commit)$(git_prompt_status)${_return_status} '
local _return_status="%{$fg_bold[red]%}%(?..⍉ )%{$reset_color%}"

# Git Status Indicators configuration
ZSH_THEME_GIT_PROMPT_SHA_BEFORE="%{$fg[yellow]%}"
ZSH_THEME_GIT_PROMPT_SHA_AFTER="%{$reset_color%} "

ZSH_THEME_GIT_PROMPT_PREFIX="%{$fg[green]%} "
ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%}"
ZSH_THEME_GIT_PROMPT_DIRTY=" %{$fg[red]%}✗%{$reset_color%} "
ZSH_THEME_GIT_PROMPT_UNTRACKED="%{$fg[white]%}◒ "
ZSH_THEME_GIT_PROMPT_CLEAN=" "
ZSH_THEME_GIT_PROMPT_ADDED="%{$fg[cyan]%}✓ "
ZSH_THEME_GIT_PROMPT_MODIFIED="%{$fg[yellow]%}△ "
ZSH_THEME_GIT_PROMPT_DELETED="%{$fg[red]%}✖ "
ZSH_THEME_GIT_PROMPT_RENAMED="%{$fg[blue]%}➜ "
ZSH_THEME_GIT_PROMPT_UNMERGED="%{$fg[cyan]%}§ "
ZSH_THEME_GIT_PROMPT_AHEAD="%{$fg[blue]%}▲ "

ZSH_THEME_GIT_TIME_SINCE_COMMIT_SHORT="%{$fg[white]%}"
ZSH_THEME_GIT_TIME_SHORT_COMMIT_MEDIUM="%{$fg[yellow]%}"
ZSH_THEME_GIT_TIME_SINCE_COMMIT_LONG="%{$fg[red]%}"
ZSH_THEME_GIT_TIME_SINCE_COMMIT_NEUTRAL="%{$fg[white]%}"

# Get the time of the last commit on git
# Used in the prompt variable
function _git_time_since_commit() {
  # Only proceed if there is actually a commit.
  # if not, don't do anything
  if git log -1 > /dev/null 2>&1; then
    # Get the last commit time information.
    last_commit=$(git log --pretty=format:'%at' -1 2> /dev/null)
    now=$(date +%s)
    seconds_since_last_commit=$((now-last_commit))

    # Totals of minute and hours
    minutes=$((seconds_since_last_commit / 60))
    hours=$((seconds_since_last_commit/3600))

    # Sub-hours and sub-minutes if applicable
    days=$((seconds_since_last_commit / 86400))
    sub_hours=$((hours % 24))
    sub_minutes=$((minutes % 60))

    if [ $hours -gt 24 ]; then
      commit_age="${days}d "
    elif [ $minutes -gt 60 ]; then
      commit_age="${sub_hours}h${sub_minutes}m "
    else
      commit_age="${minutes}m "
    fi
    if [[ -n $(git status -s 2> /dev/null) ]]; then
      if [ "$hours" -gt 4 ]; then
        COLOR="$ZSH_THEME_GIT_TIME_SINCE_COMMIT_LONG"
      elif [ "$minutes" -gt 30 ]; then
        COLOR="$ZSH_THEME_GIT_TIME_SHORT_COMMIT_MEDIUM"
      else
        COLOR="$ZSH_THEME_GIT_TIME_SINCE_COMMIT_SHORT"
      fi
    else
      COLOR="$ZSH_THEME_GIT_TIME_SINCE_COMMIT_NEUTRAL"
    fi

    echo "$COLOR$commit_age%{$reset_color%}"
  fi
}
```

### `.zshrc`

```bash
export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="kosori"

plugins=(
  gh
  git
  git-trim
  last-working-dir
  zsh-autosuggestions
  zsh-syntax-highlighting
)

source $ZSH/oh-my-zsh.sh

# ls aliases
alias l='ls -lh'
alias ls='eza --icons'
alias ll='eza -1 -a --icons'
alias la='eza -a --icons'
alias lm='ls -m'
alias lr='ls -R'
alias lg='ls -l --group-directories-first'

# cd aliases
alias ..="cd ../";
alias ...="cd ../..";
alias ..l="cd ../ && ll";
alias de="cd ~/Desktop";
alias dw="cd ~/Downloads";
alias dd="cd ~/Developer";
alias d="cd ~/Developer && cd ";

# git aliases
alias gi="git init";
alias gfr="git remote update";
alias gac="git add . && git commit -a -m ";
alias glog="git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --branches";
alias gdm="git diff | pbcopy; open raycast://ai-commands/git-commit-message --background";

# npm aliases
alias ni="npm install";
alias nid="npm install -D";
alias nu="npm uninstall";
alias nr="npm run ";
alias nrs="npm run start -s --";
alias nrb="npm run build -s --";
alias nrd="npm run dev -s --";
alias nrdp="npm run develop -s --";
alias nrl="npm run lint -s --";
alias nrlf="npm run lint:fix -s --";
alias nrc="npm run commit -s --";
alias rmnm="rm -rf node_modules";
alias flush-npm="rm -rf node_modules && npm i && echo NPM is done ✅";
alias npm-update="npx npm-check-updates -i";

# pnpm aliases
alias p="pnpm"
alias pi="pnpm install";
alias pa="pnpm add";
alias pad="pnpm add -D";
alias pr="pnpm rm";
alias flush-pnpm="rm -rf node_modules && pnpm i && echo PNPM is done ✅";
alias pnpm-update="pnpx npm-check-updates -i";

# yarn aliases
alias yar="yarn run";
alias yas="yarn start";
alias yab="yarn build";
alias yal="yarn lint:fix";
alias yac="yarn commit";

# other aliases
alias c="code .";
alias cls="clear";
alias cat="bat";
alias md="mkdir ";
alias pg="echo 'Pinging Google' && ping www.google.com";
alias lz="lazygit";
alias yz="yazi";
alias gt="git-trim";
alias n="nvim";
alias zshrc="nvim ~/.zshrc";
alias notes="cd ~/obsidian-vault/notes/ && nvim";
alias bashrc="nvim ~/.bashrc";
alias nvimdir="cd ~/.config/nvim";
alias sshdir="cd ~/.ssh";
alias topten="history | sort -rn | head";
alias myip="curl http://ipecho.net/plain; echo";
alias dirs="dirs -v | head -10";
alias usage="du -h -d1";
alias update="source ~/.zshrc";
alias runp="lsof -i ";
alias copy="pbcopy"; # macOS => pbcopy | Linux => xclip
alias paste="pbpaste"; # macOS => pbpaste | Linux => xclip -o
alias bubu="brew update && brew upgrade && brew cleanup";
# alias bubu="sudo apt update -y && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y && sudo apt clean -y";
alias spt="spotify_player";
alias set-title="kitty @ set-tab-title -m 'state:active'";

# funtions
# Get the latest commits since last merge
function extract_merge_commit_logs() {
  local current_branch=$(git rev-parse --abbrev-ref HEAD)
  local latest_merge_commit=$(git log --merges --first-parent $current_branch --pretty=format:'%H' -n 1)
  local latest_commit=$(git log --pretty=format:%H -n 1 $current_branch)

  if [ -n "$latest_merge_commit" ]; then
      git log --pretty=format:"%s" $latest_merge_commit..$current_branch
  else
      echo "No merge commit found in the current branch."
  fi
}

# Get the latest commits and changes since last merge
function extract_merge_commit_logs_with_diff() {
  local current_branch=$(git rev-parse --abbrev-ref HEAD)
  local latest_merge_commit=$(git log --merges --first-parent $current_branch --pretty=format:'%H' -n 1)
  local latest_commit=$(git log --pretty=format:%H -n 1 $current_branch)

  if [ -n "$latest_merge_commit" ]; then
      git log --pretty=format:%h:%s $latest_merge_commit..$current_branch | while read commit; do
          hash=$(echo $commit | cut -d: -f1)
          msg=$(echo $commit | cut -d: -f2-)
          echo "$msg"
          git show --pretty="" --name-only $hash
          git show --pretty="" --color $hash
      done
  else
      echo "No merge commit found in the current branch."
  fi
}

# volta
# volta end

# lazygit
# lazygit end
```
