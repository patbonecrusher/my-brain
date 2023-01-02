---
creation date: 2023-01-01 23:22
modification date: Sunday, 1st January 2023, 23:22:02
tags: today_i_leaned, computer/raspberry_pi
---

# How to install WiringPi to raspbian

WiringPi has been deprecated and must be compiled manually

```shell
git clone https://github.com/WiringPi/WiringPi --depth 1
cd WiringPi/
./build
gpio readall
```