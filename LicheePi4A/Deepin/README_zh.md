# Deepin preview LPi4A 测试报告

## 测试环境

### 系统信息

- 系统版本：Deepin preview 20240815
- 下载链接：https://cdimage.deepin.com/RISC-V/preview-20240815-riscv64/deepin-23-beige-preview-riscv64-th1520-20240815-132955.tar.xz
- 参考安装文档：https://cdimage.deepin.com/RISC-V/preview-20240517-riscv64/README.md

### 硬件信息

- Lichee Pi 4A (8G RAM + 32GB eMMC)
- 电源适配器
- USB to UART 调试器一个

## 安装步骤

注：deepin 的官方站点连接速度较慢，推荐使用一些镜像站点，如[齐鲁工业大学](https://mirrors.qlu.edu.cn/deepin-cd/deepin-cd/RISC-V/preview-20240815-riscv64/)

### 获取 u-boot

官方压缩包内不附带 u-boot，需要自己获取，地址为：https://cdimage.deepin.com/RISC-V/preview-20240815-riscv64/uboot-th1520-revyos.zip

根据 ram 大小自行选择是否需要 16g 的版本。

如果使用 8GB 版本的 LicheePi 4A，请使用 `light_lpi4a/u-boot-with-spl.bin`

如果使用 16GB 版本的 LicheePi 4A，请使用 `light_lpi4a_16g/u-boot-with-spl.bin`


### 刷写 bootloader

解压安装套件。
刷入 u-boot 与 boot。

```bash
tar -xvf deepin-23-beige-preview-riscv64-th1520-20240815-132955.tar.xz
sudo fastboot flash ram u-boot-with-spl.bin
sudo fastboot reboot
sudo fastboot flash uboot u-boot-with-spl.bin
sudo fastboot flash boot deepin-th1520-riscv64-stable-desktop-installer.boot.ext4
```

### 刷写镜像

将 root 分区刷入 eMMC 中。

```bash
sudo fastboot flash root deepin-th1520-riscv64-stable-desktop-installer.root.ext4
```

### 登录系统

重启系统后可见安装界面。

默认用户名：`root`
密码：`deepin`

## 预期结果

系统正常启动，能够通过板载串口登录。

## 实际结果

AON 固件不正常，无法启动。

### 如何修复

从 RevyOS 借个 AON 固件，扔进 boot 分区，然后刷入就工作了。

你可以从此处获取到aon固件： [https://mirror.iscas.ac.cn/revyos/extra/images/lpi4a/20240720/boot-lpi4a-20240720_171951.ext4.zst](https://mirror.iscas.ac.cn/revyos/extra/images/lpi4a/20240720/boot-lpi4a-20240720_171951.ext4.zst)

```bash
sudo losetup -P boot-lpi4a-20240720_171951.ext4
sudo losetup boot-lpi4a-20240720_171951.ext4
sudo losetup -f boot-lpi4a-20240720_171951.ext4
sudo fdisk -l
mkdir mnt
sudo mount /dev/loop0 mnt
ls mnt
cp mnt/light_aon_fpga.bin .
sudo umount mnt
sudo losetup -f deepin-th1520-riscv64-stable-desktop-installer.boot.ext4
sudo mount /dev/loop1 mnt
sudo rm mnt/light_aon_fpga.bin
sudo cp light_aon_fpga.bin mnt/
sudo umount mnt
sudo losetup -d /dev/loop1
sudo fastboot flash ram light_lpi4a/u-boot-with-spl.bin
sudo fastboot reboot
sudo fastboot flash boot deepin-th1520-riscv64-stable-desktop-installer.boot.ext4

```

见 [issue](https://github.com/linuxdeepin/developer-center/issues/10829)

### 启动信息

屏幕录像（登录系统）：
等待官方修复中...

```log
deepin-riscv64-th1520 login: root
Password:
Verification successful
Linux deepin-riscv64-th1520 5.10.113-th1520 #1 SMP PREEMPT Wed Apr 24 13:12:14 UTC 2024 riscv64
Welcome to Deepin 23 GNU/Linux

    * Homepage:https://www.deepin.org/

    * Bugreport:https://bbs.deepin.org/


root@deepin-riscv64-th1520:~# cat /etc/os-release 
PRETTY_NAME="Deepin 23"
NAME="Deepin"
VERSION_ID="23"
VERSION="23"
ID=deepin
HOME_URL="https://www.deepin.org/"
BUG_REPORT_URL="https://bbs.deepin.org"
VERSION_CODENAME=beige
root@deepin-riscv64-th1520:~# uname -a
Linux deepin-riscv64-th1520 5.10.113-th1520 #1 SMP PREEMPT Wed Apr 24 13:12:14 UTC 2024 riscv64 GNU/Linux
root@deepin-riscv64-th1520:~# cat /proc/cpuinfo
processor       : 0
hart            : 0
isa             : rv64imafdcvsu
mmu             : sv39
cpu-freq        : 1.848Ghz
cpu-icache      : 64KB
cpu-dcache      : 64KB
cpu-l2cache     : 1MB
cpu-tlb         : 1024 4-ways
cpu-cacheline   : 64Bytes
cpu-vector      : 0.7.1

processor       : 1
hart            : 1
isa             : rv64imafdcvsu
mmu             : sv39
cpu-freq        : 1.848Ghz
cpu-icache      : 64KB
cpu-dcache      : 64KB
cpu-l2cache     : 1MB
cpu-tlb         : 1024 4-ways
cpu-cacheline   : 64Bytes
cpu-vector      : 0.7.1

processor       : 2
hart            : 2
isa             : rv64imafdcvsu
mmu             : sv39
cpu-freq        : 1.848Ghz
cpu-icache      : 64KB
cpu-dcache      : 64KB
cpu-l2cache     : 1MB
cpu-tlb         : 1024 4-ways
cpu-cacheline   : 64Bytes
cpu-vector      : 0.7.1

processor       : 3
hart            : 3
isa             : rv64imafdcvsu
mmu             : sv39
cpu-freq        : 1.848Ghz
cpu-icache      : 64KB
cpu-dcache      : 64KB
cpu-l2cache     : 1MB
cpu-tlb         : 1024 4-ways
cpu-cacheline   : 64Bytes
cpu-vector      : 0.7.1
```


## 测试判定标准

测试成功：实际结果与预期结果相符。

测试失败：实际结果与预期结果不符。

## 测试结论

CFH
