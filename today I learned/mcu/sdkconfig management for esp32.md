---
creation date: 2024-04-09 22:28
modification date: Tuesday, 9th April 2024, 22:28:22
tags: today_i_leaned
---

## Using `sdkconfig.defaults`[](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/kconfig.html#using-sdkconfig-defaults "Permalink to this headline")

In some cases, for example, when the `sdkconfig` file is under revision control, it may be inconvenient for the build system to change the `sdkconfig` file. The build system offers a solution to prevent it from happening, which is to create the `sdkconfig.defaults` file. This file is never touched by the build system, and can be created manually or automatically. It contains all the options which matter to the given application and are different from the default ones. The format is the same as that of the `sdkconfig` file. `sdkconfig.defaults` can be created manually when one remembers all the changed configuration, or it can be generated automatically by running the `idf.py save-defconfig` command.

Once `sdkconfig.defaults` is created, `sdkconfig` can be deleted or added to the ignore list of the revision control system (e.g., the `.gitignore` file for `git`). Project build targets will automatically create the `sdkconfig` file, populate it with the settings from the `sdkconfig.defaults` file, and configure the rest of the settings to their default values. Note that during the build process, settings from `sdkconfig.defaults` will not override those already in `sdkconfig`. For more information, see [Custom Sdkconfig Defaults](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-guides/build-system.html#custom-sdkconfig-defaults).