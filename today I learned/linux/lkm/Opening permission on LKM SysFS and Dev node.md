---
creation date: 2022-12-20 22:38
modification date: Tuesday, 20th December 2022, 22:38:21
tags: today_i_leaned, engineering, engineering/coding, engineering/coding/linux, engineering/embedded, engineering/coding/linux/lkm 
---

# Opening permission on LKM SysFS and Dev node

## User Access to the Device using Udev Rules

By default, sudo is required to access LKM sysFS/dev nodes.  The linux kernel won't let you set rw for any sysFS/dev nodes.

To address this issue, you can use an advanced feature of Linux called _udev rules_ that enables you to customize the behavior of the udevd service. This service gives you some user-space control over devices on your Linux system.

### Preparation
For the following, lets assume we have an LKM with a DEVICE NAME of mychardev and a CLASS NAME of foobar.

For example, to give user-level access your **mychardev** device, the first step is to identify the sysfs entry for the device. You can achieve this by using a simple find:

```
user@linuxdistro:/sys# find . -name "mychardev"
./devices/virtual/foobar/mychardev
./class/foobar/mychardev   
./module/mychardev

```

We then need to identify the KERNEL and SUBSYSTEM values about which to write the rule. You can use the **udevadm** command to perform this task:  

```
user@linuxdistro:~$ udevadm info -a -p /sys/class/foobar/mychardev
Udevadm info starts with the device specified by the devpath and then walks up the chain of parent devices. It prints for every device found, all possible attributes in the udev rules key format. A rule to match, can be composed by the attributes of the device and the attributes from one single parent device.  
	looking at device '/devices/virtual/foobar/mychardev':
		KERNEL=="mychardev"
		SUBSYSTEM=="foobar"
		DRIVER==""
```

### Creating the rules

The rules are contained in the **/etc/udev/rules.d** directory. A new rule can be added as a file using these values, where the file begins with a priority number. 

#### For the main dev node

Using a name such as **99-mychardev.rules** creates a new rule with the lowest priority, so that it does not interfere with other device rules. The rule can be written as the following snippets and placed in the **/etc/udev/rules.d** directory as follows:

##### open the new file for editing
```shell
sudo vi /etc/udev/rules.d/99-mychardev.rules
```

##### enter the following in the file
```r
# Rules file for the mychardev device driver
KERNEL=="mychardev", SUBSYSTEM=="foobar", MODE="0666"
```

#### For sysfs node

##### open the new file for editing
```shell
sudo vi /etc/udev/rules.d/98-mychardev-sysfs.rules
```

##### enter the following in the file
```r
# Rules file for the mychardev device driver sysfs node
ACTION=="add", SUBSYSTEM=="foobar", KERNEL=="mychardev", RUN+="/bin/chmod a+rw /sys/path/to/sysfs/node/file"
```

### Reloading the rules

```shell
sudo udevadm control --reload-rules
```

### Conclusion

Next time you load your kernel driver using `sudo insmod mychardev.ko` the file(s) will now have the proper permission and will be accessible without using `sudo`.

---
#### References
[Writing a character driver](http://derekmolloy.ie/writing-a-linux-kernel-module-part-2-a-character-device/)
