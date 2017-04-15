Part of these tools are commercial, so I can't put their binaries here.

# bootice.exe 

Boot sector management, support including GRUB4DOS, GRUB2, NTLDR, BOOTMGR, etc. Also able to manage disk/partition and edit sector. But, notice that the grub2 image built in this software doesn't contain NTFS mod, so your `grub.cfg` must sit in FAT, EXFAT, EXT2 or other supported filesystem.

# easybcd.exe

Modify your windows BOOTMGR configuration, now included in bootice.

# diskgenius

A powerful Chinese disk/partition tool, also able to recover partitions and data.

# ghost

If you just want to recover image.

# PE.iso

Live cd to rescue Windows, version 3 (win7-like), 4 (win8-like), 5 (win8.1-like). I randomly choose [this one](https://eastonlee.b0.upaiyun.com/PE.iso), it's a very old one, but successfully booted by GRUB2, I found not every customized PE.iso is bootable by GRUB2.

# various_windows.iso

Install Windows OS.

# various_linux.iso 

Rescue, install or hack a PC.

# super_grub2_disk_hybrid_2.02s8.iso 

It probes and lists all possibly bootable OSes.