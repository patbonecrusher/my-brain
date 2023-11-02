---
creation date: 2023-11-01 21:27
modification date: Wednesday, 1st November 2023, 21:27:36
tags: today_i_leaned
---

1. Inside Prezto's base dir, create a dir called `contrib`.
2. Inside this `contrib` dir, `git clone` the `conda-zsh-completion` plugin.
3. In your `~/.zpreztorc` file, add `conda-zsh-completion` to `zstyle ':prezto:load' pmodule`.
4. Restart your terminal.

To update the plugin, `cd` into its dir and do `git pull`.