---
creation date: 2022-11-16 10:01
modification date: Wednesday 16th November 2022 10:01:48
tags: engineering/devops/ssh, today_i_leaned
---

# Remove an entry from the known-hosts

To remove an entry for a specific site or IP from the known_hosts file, useful when developing with embedded devices that re-use IP address but changes signature frequently during development.

```shell
ssh-keygen -R 192.168.1.25 # IP or site name
```
