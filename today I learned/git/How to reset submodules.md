---
creation date: 2022-12-12 22:30
modification date: Monday, 12th December 2022, 22:30:57
tags: today_i_leaned, engineering/devops/git
---

# How to reset submodules

## Method 1: Reset git submodules using `foreach` command

This method is fast because it loops each submodule and runs `git reset --hard` within each module. The command is as follows.

```
$ git submodule foreach --recursive git reset --hard
```

However, it may fail in some cases, especially after a merging that removes/add submodules.

## Method 2: Reset git submodules by de-initing and initing

If method 1 does not work, we may use the second method by de-initializing the submodules and reinitializing the submodules again. This will remove all submodules and reclone them again. So it will take more time than method 1. But this can fix many problems which lead to failures of using `git reset`. The commands are as follows:

```
# unbinds all submodules
git submodule deinit -f .
# checkout again
git submodule update --init --recursive
```

The `--recursive` option makes `git` recursively do `update --init` under submodules in case these submodules also have submodules.