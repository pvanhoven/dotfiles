# Dotfiles in a Bare Git Repo

Reference (original article): https://www.atlassian.com/git/tutorials/dotfiles

## 1) Set up a bare repository for existing dotfiles

```sh
git init --bare $HOME/.cfg
alias dotfile-cfg='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

# Keep `dotfile-cfg status` readable (don’t list all of $HOME)
dotfile-cfg config --local status.showUntrackedFiles no
```

Add/commit the dotfiles you want to track (examples):

```sh
dotfile-cfg add .bashrc .vimrc .gitdotfile-cfg
dotfile-cfg commit -m "Track dotfiles"
dotfile-cfg push -u origin main
```

## 2) Clone and use the repository in other environments

```sh
git clone --bare <git-repo-url> $HOME/.dotfile-cfg
alias dotfile-cfg='/usr/bin/git --git-dir=$HOME/.dotfile-cfg/ --work-tree=$HOME'

# Checkout files from main as bare repo won't do this
dotfile-cfg checkout main

# Hide untracked `$HOME` files for this repo:
dotfile-cfg config --local status.showUntrackedFiles no
```
