---
creation date: 2022-12-06 22:14
modification date: Tuesday, 6th December 2022, 22:14:46
tags: today_i_leaned, engineering, engineering/linux, engineering/linux/dev, engineering/linux/petalinux, engineering/linux/networking
---

# Using static ip with Petalinux

Now we’re getting to the fun part of configuring the image. The first menu we see is the following:

Select the `subsystem AUTO hardware settings` menu

![](https://hackster.imgix.net/uploads/attachments/1231052/1_UKeHcnPC-wFJgikty-YbgA.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Diving into the ethernet configuration, we’ll click the following, and see the IP is set to automatic, by default.

Select the `Ethernet settings` menu

![](https://hackster.imgix.net/uploads/attachments/1231053/1_9uQNSW0xLrR2nTRGSdUEsw.png?auto=compress%2Cformat&w=740&h=555&fit=max)

![](https://hackster.imgix.net/uploads/attachments/1231054/1_CsKErv9Th8i2MG0Vlv5VWw.png?auto=compress%2Cformat&w=740&h=555&fit=max)

![](https://hackster.imgix.net/uploads/attachments/1231055/1_HGb12OThdru1m13d-8rwrw.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Uncheck the `Optain IP address automatically` menu.

We can change the automatically IP address (DHCP) to a specific static one, by hitting the spacebar, then we see the following options:

![](https://hackster.imgix.net/uploads/attachments/1231056/1_gk6TDsMhm2Q4tXzc3TqP7A.png?auto=compress%2Cformat&w=740&h=555&fit=max)

In the example above, I chose 192.168.1.7 as my static address. Obviously the gateway should be the same prefix (**192.168.1**.1).

We can now go on and build the image, using _petalinux-build_. There are numerous nice features and tweaks worth mentioning. I’ll discuss those in a future blog.

