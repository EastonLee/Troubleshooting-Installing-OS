Installing OS is a bad job, rescuing one is worse, recovering data is the worst. But most time when it comes, we have to face it.

When you update your OS or install another one, you are taking risks of failing next startup, messing up partitions or even losing valuable data.

Here I record my regular process of installing OSes.

1. Backup: Often it takes a long while but it's worth it.
1. Format a Flash Disk to FAT32/exFAT, this is for compatibility of GRUB2, if your GRUB2 has embedded NTFS mod or other support, you can format your Flash Disk to corresponding filesystem.
1. Install GRUB2 to the boot sectors of your Flash Disk, usually you can do it easily in Linux with `grub-install` command, or in Windows with this powerful tool called **Bootice**.
1. Copy the directories `boot` and `grub` into your Flash Disk. `boot` is for GRUB2 images and configuration, `grub` is for GRUB4DOS, I just keep GRUB4DOS in case and GRUB2 is enough in theory.
1. Also carry your handy tools with you, like PE.iso and so on, I have a [list](./tools_you_need.txt) here for you.

# Install Linux

GRUB2 is able to boot Linux iso file using MEMDISK of Syslinux, but often ends up with initramfs error.

# Install Windows

## 如果要Update，保留原Windows.old

* MRB启动BOOTMGR方法：先把iso文件解压，放在某个分区根目录，并把该分区升为primary分区，并且active，PBR改为BOOTMGR，MBR改为BOOTMGR，再次启动就会自动安装了。
* grub2启动bootmgr方法：大致相同，只是在硬盘上安装grub2（要求grub2能够找到grub.cfg，最好把grub.cfg放在fat32文件系统）
* 
menuentry 'install win10'{
    insmod ntfs
    set bootmgr_path=/bootmgr
    search --set -f ${bootmgr_path}
    ntldr /bootmgr
    boot
}

* 理论上讲，可以用硬盘上的grub2直接启动iso文件，但是测试用grub2启动官方win10.iso失败，屏幕上都是黄色，伴有闪烁白色条纹。所以目前只能解压iso安装
* 不要用移动磁盘上的grub2启动硬盘上的bootmgr，win10检测到启动盘与安装盘不同，会发生“we couldn't create a new partition or locate an existing one”的错误
* 如果想把grub2装在硬盘上，请保证你的引导扇区中的grub2 image支持NTFS，或者你有一个（小）分区是fat32格式的（bootice包含的grub2 image不支持NTFS），把你的/boot目录拷入这个文件系统

## 如果不要Update，直接覆盖整个系统盘内容

* grub2本身可以启动光盘，例如PE.iso，再用ghost或者wim覆盖安装

# Random Thoughts

Windows is always a trouble maker, if a Windows 10 shuts down, it lock this disk in hibernation mode, causing other OSes suffer, you must "restart" Windows 10, and make the "restart" process stop when it's trying to restart, or forcibly shut it. If Windows is install after Linux, it will make Linux unbootable, but Linux always has Windows in mind. 

Windows is very prone to break itself, when you accidentally interrupt an update, 