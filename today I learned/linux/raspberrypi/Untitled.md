---
creation date: 2023-06-14 16:19
modification date: Wednesday, 14th June 2023, 16:19:22
tags: today_i_leaned
---

# Untitled

First time hostapd will be blocked
```
sudo systemctl unmask hostapd
sudo systemctl enable hostapd
sudo systemctl start hostapd
```


---
#### References

Good ones
```cardlink
url: https://www.cyberciti.biz/faq/debian-ubuntu-linux-setting-wireless-access-point/
title: "Debian / Ubuntu Linux: Setup Wireless Access Point (WAP) with Hostapd"
description: "I've got a spare USB Wireless Adapters (WIFI adapter/dongle) and my ISP router does not support wireless option. How do I turn my home nas server into a wireless access point (WAP) that allows wireless devices to connect to a wired network using Wi-Fi under a Debian or Ubuntu Linux operating systems without purchasing additional WPA box? How do I setup an Access Point (AP) mode Wi-Fi hotspot on a Debian or Ubuntu Linux operating systems?"
host: www.cyberciti.biz
favicon: https://www.cyberciti.biz/media/new/faq/2018/11/new_icon_amp.png
image: https://www.cyberciti.biz/media/new/faq/2021/02/frontpage.jpeg
```


How to log to a file
```cardlink
url: https://forums.raspberrypi.com/viewtopic.php?t=92859
title: "Logging hostapd output - Raspberry Pi Forums"
host: forums.raspberrypi.com
favicon: ./styles/rpi/theme/images/favicon.png
```


Others


```cardlink
url: https://www.cberner.com/2013/02/03/using-hostapd-on-ubuntu-to-create-a-wifi-access-point/
title: "Using hostapd on Ubuntu to create a wifi access point"
description: "I’ve been working on an autonomous hexacopter, which has a Pandaboard ES running Ubuntu on it, and I wanted it to setup its own wifi network in the field for easy ssh access. Turns out this is pretty simple to do, but you need to configure several different daemons to get it working right.1. Check your wifi card You’ll need a wifi card that supports master mode, if you’re going to create an access point with it."
host: www.cberner.com
image: https://www.cberner.com/images/logo.png
```


```cardlink
url: https://github.com/gh0x0st/spawning_access_points/blob/master/2.4GHz-WPA2-hostapd.conf
title: "spawning_access_points/2.4GHz-WPA2-hostapd.conf at master · gh0x0st/spawning_access_points"
description: "Leveraging kali Linux, hostapd and dnsmasq to spawn effective access points for wireless penetration tests. - spawning_access_points/2.4GHz-WPA2-hostapd.conf at master · gh0x0st/spawning_access_points"
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://opengraph.githubassets.com/5158325471261600b04baf46f1e826e1293783b74d45a1bbe4bc8aae735c2989/gh0x0st/spawning_access_points
```

