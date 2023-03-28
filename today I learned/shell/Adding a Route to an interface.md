---
creation date: 2023-03-27 21:38
modification date: Monday, 27th March 2023, 21:38:55
tags: today_i_leaned, computer/networking
---

# Adding a Route to an interface

I've directly connected my Pi to my zcu106 dev board over ethernet.

My zcu106 is set at a fixed IP address of `192.168.1.25`

I've configured my pi `eth0` to be set:
``` shell
sudo ifconfig eth0 192.168.1.22 netmask 255.255.255.0
```

To be able to ping the development board from the pi and vice-versa, I had to add a route:

``` shell
sudo route add gw 192.168.1.1 eth0
```



---
#### References
https://unix.stackexchange.com/questions/259045/how-to-set-the-default-gateway