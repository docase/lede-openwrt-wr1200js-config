# lede-openwrt-wr1200js-config
Lede 友华WR1200js编译配置

# 配置固件大小(Flash大小)
## target/linux/ramips/dts/mt7621_youhua_wr1200js.dts
### 默认(16M)
'''
partition@50000 {
        compatible = "denx,uimage";
        label = "firmware";
        reg = <0x50000 0xfb0000>;
};
'''
### 32M
0xfb0000 -> 0x1fb0000
### 64M
0xfb0000 -> 0x3fb0000

## target/linux/ramips/image/mt7621.mk
### 默认(16M)
16064k
### 32M
16064k -> 32448k (或者略小)
### 64M
16064k -> 65216k (或者略小)

# 配置支持USB 2.0 U盘
'''
Kernel modules —> USB Support —> <*> kmod-usb-core.
Kernel modules —> USB Support —> <*> kmod-usb-ohci.
Kernel modules —> USB Support —> <*> kmod-usb-uhci.
Kernel modules —> USB Support —> <*> kmod-usb-storage. #安装usb存储设备驱动
Kernel modules —> USB Support —> <*> kmod-usb-storage-extras.
Kernel modules —> USB Support —> <*> kmod-usb-storage-uas.
Kernel modules —> USB Support —> <*> kmod-usb2.0 ##usb2.0

Kernel modules —> Block Devices —> <*>kmod-scsi-core
Kernel modules —> Block Devices —> <*>kmod-scsi-generic

Kernel modules —> Filesystems —> <*> kmod-fus
Fat16/Fat32
Kernel modules —> Filesystems —> <*> kmod-fs-vfat(FAT16 / FAT32 格式 选择)
EXT4
Kernel modules —> Filesystems —> <*> kmod-fs-ext4 (移动硬盘EXT4格式选择)
exFat
Kernel modules —> Filesystems —> <*> kmod-fs-exfat

Kernel modules —> Native Language Support —> <*> kmod-nls-cp437
Kernel modules —> Native Language Support —> <*> kmod-nls-iso8859-1
Kernel modules —> Native Language Support —> <*> kmod-nls-utf8

Base system —> <*>block-mount
'''

