# cd-bookmark
[![OSS Lifecycle](https://img.shields.io/osslifecycle/erikw/cd-bookmark)](https://github.com/Netflix/osstracker)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

## FORK
This is a maintained fork of [mollifier/cd-bookmark](https://github.com/mollifier/cd-bookmark) that adds the following features:
* [`$XDG_CONFIG_HOME` support](https://github.com/mollifier/cd-bookmark/pull/5)
* [-d delete command](https://github.com/mollifier/cd-bookmark/pull/7)
* [bash support](https://github.com/mollifier/cd-bookmark/pull/8)

Migrating from [bashmarks](https://github.com/huyng/bashmarks)? Then the following aliases will make you feel at home:

```bash
alias g='cd-bookmark -c'
alias s='cd-bookmark -a'
alias l='cd-bookmark -l'
alias e='cd-bookmark -e'
alias p='cd-bookmark -p'
alias d='cd-bookmark -d'
```

### Fork maintainance notes:
```console
$ git rebase -ir upstream/master
```

## Synopsis
zsh and bash plugin to bookmark directories to cd.

Inspired by [mokemokechicken post](http://qiita.com/mokemokechicken/items/69af0db3e2cd27c1c467) and shell script in the post.

This plugin is forked from the script. The original script is licensed under the [MIT License](http://mokemokechicken.mit-license.org/).

## How to set up

### Manually install

Put cd-bookmark and _cd-bookmark files somewhere in your $fpath and add the following line to your .zshrc:

```
autoload -Uz cd-bookmark
```

#### For example

```
# download all files
% cd /path/to/dir
% git clone https://github.com/erikw/cd-bookmark.git
```

And add the following lines to your .zshrc:

```
fpath=(/path/to/dir/cd-bookmark(N-/) $fpath)

autoload -Uz cd-bookmark
```

### Installing using Antigen
If you use [Antigen](https://github.com/zsh-users/antigen), add the following line to your .zshrc:

```
antigen bundle erikw/cd-bookmark
```

You can set alias to this function.
e.g.

```
alias cdb='cd-bookmark'
```

#### Bash
For bash users, put this in your shell initialization file (typically `$HOME/.bashrc`):
```
source path/to/dir/cd-bookmark/cd-bookmark
```

## Usage


```
# 1st form
% cd-bookmark -a [BOOKMARK_ID]

# or
# 2nd form
% cd-bookmark [-c] BOOKMARK_ID

# or
# 3rd form
% cd-bookmark [-l]
```

In the 1st form, add current directory to bookmark with <var>BOOKMARK\_ID</var>.
<var>BOOKMARK\_ID</var> is used as a key in bookmark.

In the 2nd form, find directory by <var>BOOKMARK\_ID</var> and change directory to it. In this form, you can add relative path from bookmark real path at the end of BOOKMARK\_ID (see example below).

In the 3rd form, list current bookmark.

## Options
* `-a` <var>[BOOKMARK\_ID]</var>  add current directory to bookmark<br />
                                with no BOOKMARK\_ID, automatically use free ID number as BOOKMARK\_ID
* `-c` <var>BOOKMARK\_ID</var>   change directory which is identified by BOOKMARK\_ID
* `-d` <var>BOOKMARK\_ID</var>   delete directory which is identified by BOOKMARK\_ID
* `-l`                           list bookmark
* `-e`                           edit bookmark file
* `-p` <var>BOOKMARK\_ID</var>   display bookmark real path for BOOKMARK\_ID
* `-h`                           display this help and exit

## Variables
The location of the bookmarks list file depends on the envionment's configuration. The file is searched in the following order:

1. `$CD_BOOKMARK_FILE` -  if it is set. This has highest precedence. Thus you can set this to override to custom location.
1. `$XDG_CONFIG_HOME/cd-bookmarks/bookmarks` - if the directory `cd-bookmarks/` exist. Note that `$XDG_CONFIG_HOME` defaults to `$HOME/.config`
1. `$HOME/.cdbookmark` - fall back to old default $HOME/.cdbookmark


## Examples

```
# Current directory is '/home/mollifier/work'.
% pwd
/home/mollifier/work

# Add current directory to bookmark. It's bookmark ID is 'work'.
% cd-bookmark -a work

# cd somewhere.
% cd

# Back to 'work' directory.
% cd-bookmark work
% pwd
/home/mollifier/work

# Add another directory to bookmark.
% cd /home/mollifier/tmp
% cd-bookmark -a tmp

# To show current bookmark, run cd-bookmark without any options or with -l option.
% cd-bookmark
tmp|/home/mollifier/tmp
work|/home/mollifier/work

# You can add relative path from bookmark real path at the end of BOOKMARK_ID.
% cd-bookmark work/project/zsh
% pwd
/home/mollifier/work/project/zsh

# To edit bookmark, run cd-bookmark with -e option.
% cd-bookmark -e
# Open bookmark file with $EDITOR (vim, emacs, etc.), so you can edit bookmark.

# To delete a bookmark, run cd-bookmark with -d option.
% cd-bookmark -d work
```

