---
creation date: 2022-11-13 22:15
modification date: Sunday 13th November 2022, 22:15:08
tags: engineering, engineering/coding, engineering/coding/webpack, today_i_leaned
---

# pahole-flags: compile error

If you see the following when building an LKM on Linux:
```shell
make -C /lib/modules/5.15.0-48-generic/build/ M=/home/pat/fpga_lkm/src modules make[1]: Entering directory '/usr/src/linux-headers-5.15.0-48-generic' ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script make[1]: Leaving directory '/usr/src/linux-headers-5.15.0-48-generic'
```

Install the dwarves package:

```shell
sudo apt-get install dwarves
```