---
creation date: 2022-12-06 22:25
modification date: Tuesday, 6th December 2022, 22:25:34
tags: today_i_leaned, engineering/devops/git
---

# Side-by-side diff in a terminal

```
npm install -g git-split-diffs
git config --global core.pager "git-split-diffs --color | less -RFX"
```