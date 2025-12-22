---
title: Dot Files
nav_order: 5
---

# Dot Files

This document explains dot file configurations used for development tools.

## .gitconfig

This file configures Git version control settings.

### Configuration File

```ini
[user]
	name = Shaurita D. Hutchins
	email = sdhutchins@uab.edu
[push]
	default = simple
[credential]
	helper = store
[color]
  # Color everything.
  ui = auto
[log]
  # Use abbrev SHAs whenever possible/relevant instead of full 40 chars
  abbrevCommit = true
  # Automatically --follow when given a single path
  follow = true
  # Disable decorate for reflog
  # (because there is no dedicated `reflog` section available)
  decorate = false
[color "branch"]
  current = bold magenta
  upstream = bold blue
  local = yellow bold 
  remote = green bold
[color "diff"]
  # Color syntax: <foreground> <background>
  # So "normal red" is normal foreground, red background
  # BUT bold is a modifier, so "bold green red" means
  #   "bold green" foreground, red background
  whitespace = red reverse
  plain = black
  meta = cyan
  frag = magenta bold
  old = red
  new = green
  commit = yellow
[color "status"]
  # Options:
  # header: the header text of the status message
  # added/updated: added but not committed
  # changed: changed but not added in the index
  # untracked
  # nobranch: the color the "no branch" warning is shown in (default red)
  added = yellow # files deleted with "git rm" are this color too
  changed = green # deleted items NOT done with "git rm" are this color too
  untracked = cyan
[alias]
  lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
[bash-it]
  hide-status = 1
  hide-dirty = 1
```

### High-Level Overview

#### User Information
- **Name & Email**: Sets your identity for commits (name and UAB email address)

#### Push Behavior
- **Default**: Uses "simple" push mode, which only pushes the current branch to its upstream branch if they have the same name

#### Credentials
- **Helper**: Stores credentials in plain text (useful for avoiding repeated password prompts)

#### Color Configuration
- **UI**: Enables automatic color output for Git commands
- **Branch Colors**: Different colors for current branch (magenta), upstream (blue), local (yellow), and remote (green) branches
- **Diff Colors**: Color-coded diff output showing:
  - Whitespace issues (red)
  - Old changes (red)
  - New changes (green)
  - Commit info (yellow)
- **Status Colors**: Color-coded `git status` output:
  - Added files (yellow)
  - Changed files (green)
  - Untracked files (cyan)

#### Log Configuration
- **Abbrev Commit**: Shows shortened commit hashes instead of full 40-character hashes
- **Follow**: Automatically follows file renames when viewing log for a single file path
- **Decorate**: Disables branch/tag decoration in reflog output

#### Aliases
- **lg**: Custom log command that shows a graph view with colored, formatted output including commit hash, branch info, commit message, relative date, and author

#### Bash-It Integration
- **Hide Status/Dirty**: Hides Git status indicators in the bash prompt (useful for cleaner terminal appearance)

## .bash_profile

This file configures the Bash shell environment, including environment variables, PATH settings, and shell aliases.

### Configuration File

```bash
# .bash_profile

# Source bashrc for aliases and functions
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi

# ============================================================================
# Environment Variables
# ============================================================================

# PATH Configuration
PATH=$PATH:$HOME/.local/bin:$HOME/bin:$HOME/learnings_journal/vscode_remote_tunnel
export PATH

# OnDemand Development Paths
export OOD_DEV="/data/user/shutchin/ondemand/dev"
export OOD_OUT="/data/user/shutchin/ondemand/batch_connect/dev"

# Singularity Configuration
export SINGULARITY_CACHEDIR=$HOME/singularity/cache
export SINGULARITY_TMPDIR=$HOME/singularity/tmp

# ============================================================================
# Git Aliases
# ============================================================================

alias gbranches='git branch --list'
alias gfetch='git fetch --all'
alias gstat='git status'
alias gcommit='git commit -m'

# ============================================================================
# Navigation Aliases
# ============================================================================

alias home='cd $HOME'
alias ..='cd ..'
alias ...='cd ../../'
alias ....='cd ../../../'
alias .....='cd ../../../../'
alias .4='cd ../../../../'
alias .5='cd ../../../../../'
alias cd..='cd ..'
alias ood-dev='cd $OOD_DEV'
alias ood-out='cd $OOD_OUT'

# ============================================================================
# File and Directory Listing Aliases
# ============================================================================

alias ls='ls --color=auto'
alias ll='ls -la'
alias l.='ls -d .* --color=auto'
alias dir='ls -lah --color=auto'
alias pwd='pwd -P'

# ============================================================================
# Date and Time Aliases
# ============================================================================

alias now='date +"%T"'
alias nowtime=now
alias nowdate='date +"%d-%m-%Y"'

# ============================================================================
# Utility Aliases
# ============================================================================

alias h='history'
alias reload='source $HOME/.bash_profile'
alias wget='wget -c'
# alias mkdir='mkdir -pv'  # Commented out

# ============================================================================
# Application/Tool Aliases
# ============================================================================

alias nextflow='/data/project/worthey_lab/tools/nextflow/nextflow-22.10.7/nextflow'
alias ncbiftp='ftp ftp.ncbi.nlm.nih.gov'

# ============================================================================
# SLURM Job Management Aliases
# ============================================================================

alias myjobs='squeue -u $USER --format="%i|%P|%j|%u|%t|%M|%D|%R" | awk -F"|" '\''{ color = ($5 == "R") ? "\033[0;32m" : ($5 == "PD") ? "\033[0;33m" : "\033[0;31m"; printf "%s|%s|%s|%s|%s%s\033[0m|%s|%s|%s\n", $1, $2, $3, $4, color, $5, $6, $7, $8 }'\'' | column -t -s "|"'
alias killmyjobs='scancel -u $USER'
alias modrestore='module --initial_load restore'

# ============================================================================
# Module System Aliases
# ============================================================================

alias mavail='module avail'
alias mload='module load'
alias mlist='module list'
alias mspider='module -t spider'
```

### High-Level Overview

#### Bashrc Integration
- **Source**: Automatically sources `.bashrc` if it exists, ensuring aliases and functions from that file are available

#### Environment Variables
- **PATH**: Adds custom directories to PATH including local bin, home bin, and VS Code remote tunnel
- **OnDemand Development**: Sets paths for OnDemand development and batch connect output directories
- **Singularity**: Configures cache and temporary directories for Singularity container operations

#### Git Aliases
- **gbranches**: Lists all Git branches
- **gfetch**: Fetches from all remotes
- **gstat**: Shows Git status
- **gcommit**: Quick commit with message

#### Navigation Aliases
- **Quick navigation**: Shortcuts for going up directory levels (`..`, `...`, etc.)
- **Project directories**: Quick access to OnDemand development directories

#### File Operations
- **Listing**: Enhanced `ls` commands with colors and various display options
- **Directory listing**: Shortcuts for listing hidden files and detailed directory contents

#### Date/Time Utilities
- **now/nowtime**: Shows current time
- **nowdate**: Shows current date in DD-MM-YYYY format

#### SLURM Job Management
- **myjobs**: Color-coded job queue display (green for running, yellow for pending, red for other states)
- **killmyjobs**: Cancels all your jobs
- **modrestore**: Restores module environment to initial state

#### Module System
- **Shortcuts**: Abbreviated commands for module operations (avail, load, list, spider)
