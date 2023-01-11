---
creation date: 2023-01-11 16:04
modification date: Wednesday, 11th January 2023, 16:04:17
tags: today_i_leaned, engineering/devops/X11, engineering/devops/ssh
---

# Enabling X11-Forwarding for SUDO or SU

When trying to open any X11 program on a remote machine over SSH as a sudo user, you may see the following:

``` shell
$ sudo xclock
[sudo] password for user: 
X11 connection rejected because of wrong authentication.
Error: Can't open display: localhost:10.0
```

This is because _X11-Forwarding_ using _SSH_ requires the correct value for the `~/.Xauthority` file and _DISPLAY_ environment variable, which is only automatically set for the users directly connecting to the remote host and not for the user that the initial user switches to.

1. Ensure you can run the X11 program as the current user.  If that doesn't work, refer to the [Enabling X11-Forwarding over SSH](Enabling%20X11-Forwarding%20over%20SSH).

2. Connect to the SSH server of your choice:
```shell
$ ssh -X remote-host
user@remote-host's password: 
Welcome to Ubuntu 20.10 (GNU/Linux 5.8.0-26-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be installed immediately.
0 of these updates are security updates.

Last login: Sun Nov  1 21:17:13 2020 from 192.168.111.27
```

3. Get the current user X authorization entry for the current display.
``` shell
$ xauth list $DISPLAY
host/unix:10  MIT-MAGIC-COOKIE-1  742d024faeb3d29a15ff06f1b8c3b21e
```

4. Get the _DISPLAY_ environment variable value:
``` shell
$ echo $DISPLAY
localhost:10.0
```

5. Switch to root or other user using *sudo* and/or *su*:
``` shell
$ sudo su -
[sudo] password for user: 
root@host:~#
```

6. Generate _~/.Xauthority_ file using _xauth_ command: (use the info obtained in step 3)
``` shell
# xauth add host/unix:10  MIT-MAGIC-COOKIE-1  742d024faeb3d29a15ff06f1b8c3b21e
```

7. Export the _DISPLAY_ environment variable value for the current user: (use the info obtained in step 4)
``` shell
# export DISPLAY=localhost:10.0
```

8. Verify that it is working:
``` shell
# xclock
```

If it works, you should see the X clock on your local computer, running from the remote machine you've ssh into.