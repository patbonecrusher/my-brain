---
creation date: 2024-01-07 21:48
modification date: Sunday, 7th January 2024, 21:48:50
tags: today_i_leaned
---
# Installing cmake from source on a Raspberry Pi

This procedure will take about an hour.

## Install:

- If another version if cmake is installed, uninstall it. A compiler such as g++ must be installed.  
    
    `sudo apt remove cmake`
    
- Prerequisite
    
    `sudo apt install libssl-dev`
    
- Download the latest archive from [https://cmake.org/download/](https://cmake.org/download/) to a directory such as your home directory.
- Extract cmake-3.19.2.tar.gz. (or later) This procedure assumes your home directory. For other versions change the version in the commands.

```shell
cd ~/
tar -zxvf cmake-3.19.2.tar.gz # directory depends on the archive version
cd cmake-3.19.2
./bootstrap
make -j 4
sudo make install
sudo ldconfig
```

    
- reboot