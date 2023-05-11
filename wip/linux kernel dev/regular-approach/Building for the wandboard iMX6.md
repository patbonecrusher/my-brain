---
creation date: 2022-12-16 22:51
modification date: Friday, 16th December 2022, 22:51:44
tags: engineering/board/wandboard, engineering/embedded/linux
---

# Building for the wandboard iMX6

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

``` shell
vagrant up
vagrant ssh

export CC=/vagrant/gcc-arm-11.2-2022.02-aarch64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-
```

### building u-boot
``` shell
git clone -b v2019.04 https://github.com/u-boot/u-boot --depth=1
cd u-boot

wget -c https://github.com/eewiki/u-boot-patches/raw/master/v2019.04/0001-wandboard-uEnv.txt-bootz-n-fixes.patch
patch -p1 < 0001-wandboard-uEnv.txt-bootz-n-fixes.patch

make ARCH=arm CROSS_COMPILE=${CC} distclean
make ARCH=arm CROSS_COMPILE=${CC} wandboard_defconfig
make ARCH=arm CROSS_COMPILE=${CC}

```

### Making the sd card

``` shell
# lsblk to find the correct sd card
export DISK=/dev/sdb
sudo dd if=/dev/zero of=${DISK} bs=1M count=10
sudo dd if=./u-boot/SPL of=${DISK} seek=1 bs=1k
sudo dd if=./u-boot/u-boot.img of=${DISK} seek=69 bs=1k

sudo sfdisk ${DISK} <<-__EOF__
1M,,L,*
__EOF__

sudo mkfs.ext4 -L rootfs ${DISK}1
sudo mount ${DISK}1 /media/rootfs/

export kernel_version=5.4.209-armv7-x65

sudo tar xfvp ./*-*-*-armhf-*/armhf-rootfs-*.tar -C /media/rootfs/
sync

sudo sh -c "echo 'uname_r=${kernel_version}' >> /media/rootfs/boot/uEnv.txt"

sudo sh -c "echo 'cmdline=video=HDMI-A-1:1024x768@60e' >> /media/rootfs/boot/uEnv.txt"

sudo cp -v ./kernelbuildscripts/deploy/${kernel_version}.zImage /media/rootfs/boot/vmlinuz-${kernel_version}

sudo mkdir -p /media/rootfs/boot/dtbs/${kernel_version}/

sudo tar xfv ./kernelbuildscripts/deploy/${kernel_version}-dtbs.tar.gz -C /media/rootfs/boot/dtbs/${kernel_version}/

sudo tar xfv ./kernelbuildscripts/deploy/${kernel_version}-modules.tar.gz -C /media/rootfs/

sudo sh -c "echo '/dev/mmcblk2p1  /  auto  errors=remount-ro  0  1' >> /media/rootfs/etc/fstab"

sync

sudo umount /media/rootfs


```
  330  sudo dd if=/dev/zero of=${DISK} bs=1M count=10
  331  export DISK=/dev/sdb
  332  sudo dd if=/dev/zero of=${DISK} bs=1M count=10
  333  #user@localhost:~$
  334  sudo dd if=./u-boot/SPL of=${DISK} seek=1 bs=1k
  335  sudo dd if=./u-boot/u-boot.img of=${DISK} seek=69 bs=1k
  336  #sfdisk >= 2.26.x
  337  sudo sfdisk ${DISK} <<-__EOF__
1M,,L,*
__EOF__

  338  lsblk
  339  sudo dd if=/dev/zero of=${DISK} bs=1M count=10
  340  lsblk
  341  sudo dd if=./u-boot/SPL of=${DISK} seek=1 bs=1k
  342  sudo dd if=./u-boot/u-boot.img of=${DISK} seek=69 bs=1k
  343  sudo sfdisk ${DISK} <<-__EOF__
1M,,L,*
__EOF__

  344  sudo mkfs.ext4 -L rootfs ${DISK}1
  345  sudo mount ${DISK}1 /media/rootfs/

---
#### references
https://forum.digikey.com/t/debian-getting-started-with-the-wandboard/12707
