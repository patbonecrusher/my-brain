---
creation date: 2024-01-08 16:04
modification date: Monday, 8th January 2024, 16:04:54
tags: today_i_leaned
---

Every now and then, I need to run some utility written in C++ on my Raspberry Pi. Now, there are powerful solutions like [crosstool-ng](https://crosstool-ng.github.io/) and others, but they require a lot of setup and time. Looking for something simpler? Then here you go:

## Prerequisites

This article expects that Xcode and [homebrew](https://brew.sh/) are installed on your Mac and that your Raspberry Pi is running Linux and set up for login via ssh.

## Step 1: Compiler and binutils

In order to compile for the Raspberry Pi, we need binutils to assemble and link binaries and a compiler that can produce code for the ARM CPU. In this step, we install [clang](https://clang.llvm.org/) as compiler and the [GNU binutils](https://www.gnu.org/software/binutils/) compiled for the hard float GNU EABI, which is what most Linux distributions run. In addition, we also install [rsync](https://rsync.samba.org/) from homebrew, which we need later:

```
brew install arm-linux-gnueabihf-binutils llvm rsync
```

## Step 2: Sysroot

In order to compile anything meaningful, we also need the libraries that come with our Raspberry Pi Linux distribution. There are multiple ways to obtain them, like using remote file systems. This is however quite slow and requires to have the Raspberry Pi online and running all the time while compiling. I found it more convenient to simply use rsync to sync the relevant directories directly to my Mac.

Run the following command in your favorite directory (e.g. your home directory):

```
export piip='fikst@192.168.15.11'
export sysroot='/Users/pat/Projects/sysroot/raspbian32'
/opt/homebrew/bin/rsync -rzLR --safe-links \
${piip}:/usr/lib/arm-linux-gnueabihf \
${piip}:/usr/lib/gcc/arm-linux-gnueabihf \
${piip}:/usr/include \
${piip}:/lib/arm-linux-gnueabihf \
${sysroot}

# I had to do this to avoid an error finding that library
(cd raspbian/lib && ln -s  arm-linux-gnueabihf/ld-linux-armhf.so.3 ld-linux-armhf.so.3)
```

## Bringing it all together

We now have all the pieces together, let’s compile our first C++ program. Save the C++ code below to a file called hello.cpp:

```c++
int main() { return 42; }
```

In order to compile it, we launch the clang compiler that we installed with Homebrew in Step 1, letting it know where to find the binutils from Step 1 and the Sysroot from Step 2:

```shell
`brew --prefix llvm`/bin/clang++ \
--target=arm-linux-gnueabihf \
-nostdinc++ \
-cxx-isystem $sysroot/usr/include/c++/10 \
-cxx-isystem $sysroot/usr/include/arm-linux-gnueabihf/c++/10 \
-isystem $sysroot/usr/include/c++/10  \
--sysroot=$sysroot \
-isystem=$sysroot/usr/include/c++/10 \
-isystem=$sysroot/usr/include/c++/10/bits \
-isystem=$sysroot/usr/include/arm-linux-gnueabihf/c++/10 \
-I$sysroot/usr/include/c++/10 \
-I$sysroot/usr/include/c++/10/bits \
-L$sysroot/usr/lib/gcc/arm-linux-gnueabihf/10 \
-L$sysroot/lib/arm-linux-gnueabihf \
-L$sysroot/usr/lib/arm-linux-gnueabihf \
-B$sysroot/usr/lib/gcc/arm-linux-gnueabihf/10 \
--gcc-toolchain=`brew --prefix arm-linux-gnueabihf-binutils` \
-o hello \
hello.cpp

armv8-rpi4-linux-gnueabihf-gcc main.c \
--sysroot=/var/lib/schroot/chroots/rpizero-bullseye-armhf \
-o main

/home/pat/x-tools/armv8-rpi4-linux-gnueabihf/bin/armv8-rpi4-linux-gnueabihf-gcc \ 
  --sysroot=/var/lib/schroot/chroots/rpizero-bullseye-armhf   
  -mcpu=cortex-a72 -mfpu=neon-fp-armv8 -mfloat-abi=hard  -o CMakeFiles/cmTC_ab883.dir/testCCompiler.c.o -c /home/pat/repos/nortis_perfusion_source/PerfusionHMI/buildp/CMakeFiles/CMakeTmp/testCCompiler.c

clang++ \
--target=armv8-rpi4-linux-gnueabihf \
-nostdinc++ \
-cxx-isystem $sysroot/usr/include/c++/10 \
-cxx-isystem $sysroot/usr/include/arm-linux-gnueabihf/c++/10 \
-isystem $sysroot/usr/include/c++/10  \
--sysroot=$sysroot \
-isystem=$sysroot/usr/include/c++/10 \
-isystem=$sysroot/usr/include/c++/10/bits \
-isystem=$sysroot/usr/include/arm-linux-gnueabihf/c++/10 \
-I$sysroot/usr/include/c++/10 \
-I$sysroot/usr/include/c++/10/bits \
-L$sysroot/usr/lib/gcc/arm-linux-gnueabihf/10 \
-L$sysroot/lib/arm-linux-gnueabihf \
-L$sysroot/usr/lib/arm-linux-gnueabihf \
-B$sysroot/usr/lib/gcc/arm-linux-gnueabihf/10 \
--gcc-toolchain=`~/x-tools/armv8-rpi4-linux-gnueabihf/bin` \
-o main \
main.c

```