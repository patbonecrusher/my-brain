If you see the following when building a LKM on Linux:
```shell
make -C /lib/modules/5.15.0-48-generic/build/ M=/home/pat/fpga_lkm/src modules make[1]: Entering directory '/usr/src/linux-headers-5.15.0-48-generic' ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script ./scripts/pahole-flags.sh: line 8: return: can only `return' from a function or sourced script make[1]: Leaving directory '/usr/src/linux-headers-5.15.0-48-generic'
```

Install the dwarves package:

```shell
sudo apt-get install dwarves
```