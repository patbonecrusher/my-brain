---
creation date: 2024-02-08 09:49
modification date: Thursday, 8th February 2024, 09:49:05
tags:
  - today_i_leaned
  - engineering/linux
  - engineering/bus/pci
---
Note: If you are not root, remember to use sudo

BAR is record of the device address starting at memory.

```
root@Ubuntu:~$ lspci -s 00:04.0 -x
00:04.0 USB controller: Intel Corporation 82801DB/DBM (ICH4/ICH4-M) USB2 EHCI Controller (rev 10)
00: 86 80 cd 24 06 00 00 00 10 20 03 0c 10 00 00 00
10: 00 10 02 f3 00 00 00 00 00 00 00 00 00 00 00 00
20: 00 00 00 00 00 00 00 00 00 00 00 00 f4 1a 00 11
30: 00 00 00 00 00 00 00 00 00 00 00 00 05 04 00 00

root@Ubuntu:~$ lspci -s 00:04.0 -v
00:04.0 USB controller: Intel Corporation 82801DB/DBM (ICH4/ICH4-M) USB2 EHCI Controller (rev 10) (prog-if 20 [EHCI])
        Subsystem: Red Hat, Inc QEMU Virtual Machine
        Physical Slot: 4
        Flags: bus master, fast devsel, latency 0, IRQ 35
        Memory at f3021000 (32-bit, non-prefetchable) [size=4K]
        Kernel driver in use: ehci-pci
root@Ubuntu:~$ grep  00:04.0 /proc/iomem
  f3021000-f3021fff : 0000:00:04.0
```

0xfff equals to 4095, which is 4K. Memory starts at 0xf3021000 is this USB device seen by CPU. This address is init during BIOS and in this example it is on BAR0. Why is BAR0?

Before that, one need to understand PCI spec, especially the below, type 0 and type 1:

[![enter image description here](https://i.stack.imgur.com/clgM1.png)](https://i.stack.imgur.com/clgM1.png)

[![enter image description here](https://i.stack.imgur.com/f7GEA.png)](https://i.stack.imgur.com/f7GEA.png)

Notice the header type is both defined at 0x0c third field, that is how BARs differ. In this example, it is 00, which means it is type 0. Thus BAR0 stores the address, which is `00 10 02 f3`. 

One may wonder why this is not exactly `f3021000`, this is because lspci goes with Little Endian. What is Endian? One may need to read "Gulliver's Travels".

BAR0 generally has three states, uninitialized, all 1s, and written address. And we now in the third since the device already init. Bit 11 ~ 4 is set to 0 at uninitialized state; Bit 3 means NP when set to 0, P when set to 1; Bit 2 ~ 1 means 32 bit when set to 00, 64 bit when set to 10; Bit 0 means memory request when set to 0, IO request when set to 1.

```
0xf3021000
====>>>>
11110011000000100001000000000000
```

From this, we can know this device is 32-bit, non-prefetchable, memory request. The uninitialized address is 32 ~ 12, since 2 ^ 12 = 4K.

For more device and vendor, one can find via [https://pcilookup.com/](https://pcilookup.com/)