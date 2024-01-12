---
creation date: 2024-01-12 14:53
modification date: Friday, 12th January 2024, 14:53:15
tags: today_i_leaned
---
Using enbassy.dev rust framework.

## On macOS

I tried to compile the example from the embassy GitHub repo:

```cardlink
url: https://github.com/embassy-rs/embassy.git
title: "GitHub - embassy-rs/embassy: Modern embedded framework, using Rust and async."
description: "Modern embedded framework, using Rust and async. Contribute to embassy-rs/embassy development by creating an account on GitHub."
host: github.com
favicon: https://github.githubassets.com/favicons/favicon.svg
image: https://opengraph.githubassets.com/b7fe603db3aa578e18819b90161fc1fc0035854ed2180ac82c926bb06e2a2bbc/embassy-rs/embassy
```

That didn't work as it depends on some linux packages.

## Using Vagrant

---
### VM Setup

In the cloned embassy repo, at the root I've added 2 files:

Vagrantfile (note that the box would have to be adjusted based on your computer architecture)
```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "jharoian3/ubuntu-22.04-arm64"
  config.vm.provision "shell", path: "bootstrap.sh"
end
```

bootstrap.sh
```
#!/bin/sh
sudo apt-get update &&
    sudo apt-get install -y curl ca-certificates build-essential &&
    su vagrant -c 'curl https://sh.rustup.rs -sSf | sh -s -- -y' &&
    cargo install probe-rs --features cli
    sudo apt-get purge -y curl &&
    sudo apt-get autoremove --purge -y &&
    sudo apt-get autoclean -y &&
    sudo apt-get clean -y &&
    sudo rm -rf /var/lib/apt/lists/* \
        /var/cache/apt/pkgcache.bin \
        /var/cache/apt/srcpkgcache.bin
```
Then to bring it up
```
vagrant up
vagrant ssh
```

---
### Accessing JTag devkit

For embassy rust to be able to download and run code on the device you need some adapter program.  I went with the probe.rs approach.  

```cardlink
url: https://probe.rs/docs/getting-started/probe-setup/
title: "probe-rs - Probe Setup"
host: probe.rs
favicon: https://probe.rs/favicon.ico
```

In the vagrant VM:
@note *The following steps should reaelly be part of the bootstrap process*

#### Install dependency
```
sudo apt update
sudo apt install -y pkg-config libusb-1.0-0-dev libftdi1-dev libudev-dev libssl-dev udev
```

#### Install probe-rs
```
cargo install probe-rs --features cli
```

#### Configure udev rules for stm board access
```
1. Download the [rules file](https://probe.rs/files/69-probe-rs.rules) and place it in /etc/udev/rules.d.
2. Run `udevadm control --reload` to ensure the new rules are used.
3. Run `udevadm trigger` to ensure the new rules are applied to already added devices.
4. sudo usermod -a -G plugdev vagrant
```

#### Testing
Log out and log back in.
Connect your devkit to your VM.

Run
```
vagrant@vagrant:/vagrant/examples/stm32h7$ probe-rs list
The following debug probes were found:
[0]: STLink V3 (VID: 0483, PID: 374e, Serial: 0030004A3432511630343838, StLink)
```
---
### Running blinky

1.  SSH on your VM
```
vagrant ssh
```
2. Navigate to the sample folder for your board familly
```
cd /vagrant/examples/stm32h7
```
3. Change the board number in Cargo.toml.  By default it is set to stm32h743bi.  My kit is the stm32h723zg
```
[dependencies]
# Change stm32h743bi to your chip name, if necessary.
embassy-stm32 = { version = "0.1.0", path = "../../embassy-stm32", features = ["defmt", "stm32h723zg", "time-driver-any", "exti", "memory-x", "unstable-pac", "chrono"] }
```
4. Compile blinky
```
cargo build --bin blinky --release
```
5. Download and run blinky on the board
```
cargo run --bin blinky --release
```

If everything went ok you should see:
```
vagrant@vagrant:/vagrant/examples/stm32h7$ cargo run --bin blinky --release
    Finished release [optimized + debuginfo] target(s) in 4.17s
     Running `probe-rs run --chip STM32H743ZITx target/thumbv7em-none-eabihf/release/blinky`
      Erasing ✔ [00:00:02] [#################################################] 128.00 KiB/128.00 KiB @ 52.80 KiB/s (eta 0s )
  Programming ✔ [00:00:06] [####################################################] 27.00 KiB/27.00 KiB @ 4.05 KiB/s (eta 0s )    Finished in 9.228s
0.000000 DEBUG flash: latency=0 wrhighfreq=0
└─ embassy_stm32::rcc::_version::flash_setup @ /vagrant/embassy-stm32/src/fmt.rs:130
0.000000 TRACE BDCR ok: 00008200
└─ embassy_stm32::rcc::bd::{impl#3}::init @ /vagrant/embassy-stm32/src/fmt.rs:117
0.000000 DEBUG rcc: Clocks { sys: Hertz(64000000), pclk1: Hertz(64000000), pclk1_tim: Hertz(64000000), pclk2: Hertz(64000000), pclk2_tim: Hertz(64000000), pclk3: Hertz(64000000), pclk4: Hertz(64000000), hclk1: Hertz(64000000), hclk2: Hertz(64000000), hclk3: Hertz(64000000), hclk4: Hertz(64000000), pll1_q: None, pll2_p: None, pll2_q: None, pll2_r: None, pll3_p: None, pll3_q: None, pll3_r: None, adc: Some(Hertz(64000000)), rtc: Some(Hertz(32000)), hsi: None, csi: None, lse: None, hse: None, per: None, rcc_pclk_d3: None }
└─ embassy_stm32::rcc::set_freqs @ /vagrant/embassy-stm32/src/fmt.rs:130
0.000000 INFO  Hello World!
└─ blinky::____embassy_main_task::{async_fn#0} @ src/bin/blinky.rs:13
0.000000 INFO  high
└─ blinky::____embassy_main_task::{async_fn#0} @ src/bin/blinky.rs:18
1.000030 INFO  low
```
