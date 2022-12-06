---
creation date: 2022-12-06 15:57
modification date: Tuesday, 6th December 2022, 15:57:19
tags: [today_i_leaned, engineering/linux/yocto]
---

# Rebuilding a specific yocto recipe

Another helpful command for working on bb file recipes is:

```bash
# the whole recipe:
petalinux-build -c <recipe> --force

# command in the recipe
petalinux-build -c <recipe> -x <bb_file section> --force
```

the bb_file_section can be "compile" for the "do_compile" section... etc