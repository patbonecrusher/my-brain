---
creation date: 2022-12-16 22:51
modification date: Friday, 16th December 2022, 22:51:44
tags: 
---

# Untitled

```
1  ls
    2  ifconfig
    3  ls
    4  cd /vagrant
    5  ls
    6  cd /vagrant
    7  ls
    8  tar xvf gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabi.tar.xz
    9  ls
   10  ./gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabi/bin/gcc
   11  ./gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabi/bin/arm-linux-gnueabi-g++ --version
   12  file --version
   13  file gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabin/bin/arm-linux-gnueabi-g++
   14  ls
   15  cat gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabi/bin/arm-linux-gnueabi-g++
   16  file gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabi/bin/arm-linux-gnueabi-g++
   17  cd /vagrant
   18  ls
   19  gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-g++ --version
   20  export CC=`pwd`gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-g++ --version
   21  export CC=`pwd`gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-
   22  $CCg++
   23  $CCgcc
   24  $CCgcc --version
   25  $CCgcc -version
   26  ${CC}gcc --version
   27  export CC=`pwd`/gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-
   28  ${CC}gcc --version
   29  git clone -b v2019.04 https://github.com/u-boot/u-boot --depth=1
   30  cd u-boot/
   31  wget -c https://github.com/eewiki/u-boot-patches/raw/master/v2019.04/0001-wandboard-uEnv.txt-bootz-n-fixes.patch
   32  patch -p1 < 0001-wandboard-uEnv.txt-bootz-n-fixes.patch
   33  make ARCH=arm CROSS_COMPILE=${CC} distclean
   34  make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
   35  apt install bison
   36  sudo apt install bison
   37  apt install bison
   38  make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
   39  sudo apt install flex
   40  make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
   41  make ARCH=arm CROSS_COMPILE=${CC} distclean
   42  make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
   43  make ARCH=arm CROSS_COMPILE=${CC}
   44  ls
   45  mv spl SPL
   46  ls -al
   47  ls SPL
   48  ls spl
   49  history
   50  cd ~
   51  mkdir u-boot
   52  cd u-boot/
   53  git clone -b v2019.04 https://github.com/u-boot/u-boot --depth=1
   54  cd u-boot/
   55  wget -c https://github.com/eewiki/u-boot-patches/raw/master/v2019.04/0001-wandboard-uEnv.txt-bootz-n-fixes.patch
   56  patch -p1 < 0001-wandboard-uEnv.txt-bootz-n-fixes.patch
   57  make ARCH=arm CROSS_COMPILE=${CC} distclean
   58  make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
   59  ls -al
   60  make ARCH=arm CROSS_COMPILE=${CC}
   61  ls
   62  cd ..
   63  ls
   64  cd ..
   65  git clone https://github.com/RobertCNelson/armv7-multiplatform ./kernelbuildscripts
   66  cd kernelbuildscripts/
   67  git checkout origin/v5.4.x -b tmp
   68  ./build_kernel.sh
   69  sudo apt install lzop
   70  ./build_kernel.sh
   71  sudo apt-get install lzma gettext pkg-config libmpc-dev u-boot-tools libncurses5-dev:arm64 libssl-dev:arm64
   72  ./build_kernel.sh
   73  vi build_kernel.sh
   74  ls dl
   75  ag arm-linux-gnueabi
   76  sudo apt install ag
   77  sudo apt install the-silver-searcher
   78  ag arm-linux-gnueabi
   79  cd ..
   80  ls
   81  ls u-boot/
   82  ls /vagrant/
   83  which gcc
   84  printenv CC
   85  arm-linux-gnueabihf-gcc-11 -march=armv7-a -c -x c /dev/null
   86  cd kernelbuildscripts/
   87  ls
   88  vi system.sh
   89  uname -m
   90  vi system.sh
   91  ./build_kernel.sh
   92  ag arm-linux-gnueabi
   93  ls
   94  vi scripts/gcc.sh
   95  vi version.sh
   96  vi scripts/gcc.sh
   97  ./build_kernel.sh
   98  vi system.sh
   99  ./build_kernel.sh
  100  vi scripts/gcc.sh
  101  ls
  102  git status
  103  git restore scripts/gcc.sh
  104  ./build_kernel.sh
  105  vi system.sh
  106  echo $CC
  107  vi system.sh
  108  ./build_kernel.sh
  109  ls
  110  history
```

---
#### references
https://forum.digikey.com/t/debian-getting-started-with-the-wandboard/12707
