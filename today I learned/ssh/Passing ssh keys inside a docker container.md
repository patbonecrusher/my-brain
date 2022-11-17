---
creation date: 2022-11-16 22:29
modification date: Wednesday 16th November 2022 22:29:16
tags: engineering/devops/ssh, engineering/docker, today_i_leaned
---

# Passing ssh keys inside a docker container

```shell
docker run -v /home/<host user>/.ssh:/home/<docker user>/.ssh <image>
```