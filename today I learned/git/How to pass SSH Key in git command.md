---
creation date: 2023-03-07 10:18
modification date: Tuesday, 7th March 2023, 10:18:26
tags: today_i_leaned, engineering/scm/git
---

# How to pass SSH Key in git command

```
$ GIT_SSH_COMMAND='ssh -i /path/to/.ssh/ssh_key' git pull # or whatever command
```