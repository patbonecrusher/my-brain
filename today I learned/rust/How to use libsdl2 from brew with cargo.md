---
creation date: 2023-12-23 13:16
modification date: Saturday, 23rd December 2023, 13:16:29
tags: today_i_leaned
---

#### Homebrew

On macOS, it's a good idea to install these via [homebrew](http://brew.sh/).

```
brew install sdl2
```

In recent versions of Homebrew, the installed libraries are usually linked into `$(brew --prefix)/lib`. If you are running an older version, the symlink for SDL might reside in `/usr/local/lib`.

To make linking libraries installed by Homebrew easier, do the following for your respective shell.

Add this line to your `~/.zshenv` or `~/.bash_profile` depending on whether you use ZSH or Bash.

```
export LIBRARY_PATH="$LIBRARY_PATH:$(brew --prefix)/lib"
```