---
creation date: 2023-05-11 17:16
modification date: Thursday, 11th May 2023, 17:16:54
tags: today_i_leaned, engineering/embedded/uboot
---

# How to list the content of partitions in u-boot

```shell
u-boot=> fatls mmc 0:0
** Unrecognized filesystem type **

u-boot=> fatls mmc 0:1
20836864 image
41463 fsl-imx8mm-evk.dtb
42243 fsl-imx8mm-evk-ak4497.dtb
41483 fsl-imx8mm-evk-ak5558.dtb
41515 fsl-imx8mm-evk-audio-tdm.dtb
21263 fsl-imx8mm-evk-inmate.dtb
41884 fsl-imx8mm-evk-m4.dtb
41961 fsl-imx8mm-evk-rm67191.dtb
41925 fsl-imx8mm-evk-root.dtb
6400 imx8mm_m4_tcm_hello_world.bin
17192 imx8mm_m4_tcm_rpmsg_lite_pingpong_rtos_linux_remote.bin
16824 imx8mm_m4_tcm_rpmsg_lite_str_echo_rtos.bin
31064 imx8mm_m4_tcm_sai_low_power_audio.bin
316072 utee-8mm
14 file(s), 0 dir(s)

u-boot=> fatls mmc 0:2
** Unrecognized filesystem type **

u-boot=> ext4ls mmc 0:2
1024 .
1024 ..
12288 lost+found
1024 usr
1024 dev
3072 lib
1024 boot
1024 tmp
1024 etc
3072 sbin
1024 var
1024 run
1024 home
1024 media
1024 proc
3072 bin
1024 sys
1024 mnt
1024 .fseventsd

u-boot=>
```