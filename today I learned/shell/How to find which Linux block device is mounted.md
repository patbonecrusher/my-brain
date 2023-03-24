---
creation date: 2023-03-23 21:07
modification date: Thursday, 23rd March 2023, 21:07:26
tags: today_i_leaned, engineering/devops, engineering/linux
---

# How to find which Linux block device is mounted

To list all block devices, run the lsblk command:  
```shell
$ sudo lsblk   
$ sudo lsblk /dev/DEVICE   
$ sudo lsblk /dev/sda
$ sudo lsblk -l
# use the [grep command](https://www.cyberciti.biz/faq/howto-use-grep-command-in-linux-unix/ "How to use grep command in Linux/ Unix with examples")/egerp command to filter out info #   
$ sudo lsblk -d | grep disk
```


We can also fine-tune information displayed by lsblk as follows to list only Linux partitions and other data:  
```shell
$ sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT
```

Pass the following -f and -m to see detailed info:  
```shell
$ sudo lsblk -f -m   $ sudo lsblk -f -m | grep ext4
```


## Listing Linux a Partition Size Larger Than 2TB

The fdisk or sfdisk command [will not list any partition size larger than 2TB](https://www.cyberciti.biz/tips/fdisk-unable-to-create-partition-greater-2tb.html). You need to use GNU parted command with GPT partitions to solve this problem. It supports Intel EFI/GPT partition tables. Partition Table (GPT) is a standard for the layout of the partition table on a physical hard disk. It is a part of the Extensible Firmware Interface (EFI) standard proposed by Intel as a replacement for the outdated PC BIOS, one of the few remaining relics of the original IBM PC. EFI uses GPT, whereas BIOS uses a Master Boot Record (MBR). In this example, list partitions on /dev/sdb using the parted command:  

```shell
$ sudo parted /dev/sdb
```


---
#### reference
https://www.cyberciti.biz/faq/linux-list-disk-partitions-command/