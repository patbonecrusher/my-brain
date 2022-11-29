---
creation date: 2022-11-28 23:23
modification date: Monday, 28th November 2022, 23:23:30
tags: engineering/devops/shell, engineering/devops/tmux, today_i_leaned
---

# Moving a running process to tmux

To move a running process to a Tmux session (requires [reptyr](https://github.com/nelhage/reptyr)):

Suspend process: press `Ctrl+Z`
Resume process in background: `bg`
Disown process: `disown %1`
Launch Tmux
Find PID: `ps a | grep <$PROCESS_NAME>`
Resume process in Tmux: `reptyr <$PID>`