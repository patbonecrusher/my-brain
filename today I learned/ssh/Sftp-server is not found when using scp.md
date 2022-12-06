---
creation date: 2022-11-16 09:31
modification date: Wednesday 16th November 2022 09:31:27
tags: engineering/devops/ssh, engineering/devops/scp, today_i_leaned
---

# sftp-server: not found when using scp

If you see the following when trying to scp a file to a remote server:
```shell
scp some_file some_server:~
/usr/libexec/sftp-server: not found
```

This is a consequence of your client machine using a very recent OpenSSH release (9.0 - check https://www.openssh.com/txt/release-9.0 for more info), which changes the scp program to use the SFTP protocol under the hood, which vanilla OpenWrt/dropbear installations do not support. To work around the problem on the client side, use the new -O (that is an uppercase letter "o") switch when invoking scp, which will cause it to fall back to the legacy behavior.

To fix:
```shell
scp -O some_file some_server:~
```