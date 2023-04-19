---
creation date: 2023-03-30 21:00
modification date: Thursday, 30th March 2023, 21:00:53
tags: today_i_leaned, engineering/embedded/esp32
---

# How to build esp32 in docker and flash device in docker

Open a shell window inside your project (*make sure you run the export.sh from esp*, or install esptools using pip):

``` shell
esp_rfc2217_server.py -v -p 4000 /dev/cu.usbserial-11110
```

In another shell, *it has to be bash as it does not work in zsh for reasons unknown* to build:
``` bash
docker run --rm -it \
	--network host \
	-v "$(pwd)":/workspace \
	-w="/workspace" \
	espressif/idf:release-v4.4 \
	idf.py \
	-p rfc2217://host.docker.internal:4000?ign_set_control \
	build flash monitor
```