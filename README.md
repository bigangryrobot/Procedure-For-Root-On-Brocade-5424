1. pop the case (required taking a torx 9 and filing the tip down a bit… stupid safety screws)
2. press the 2 switches one at a time in the upper corner to reset the bios recovery password
4. remove the flash memory module and set it to the side
3. insert the unit into the m1ke chassis and let it boot (no need to replace the cover)
4. Follow the below (look its running u-boot!)
``` 
$ connect switch-4
connect: acquiring remote port.
Connected to remote port.
Escape character is '^\'.
 
 
System RAM test using Default POST RAM Test succeeded.
 
set_bootstatus: BS_LOAD_OS, platform_idx = 5
 
Type run flash_nfs to mount root filesystem over NFS
 
Hit ESC to stop autoboot:  0
 
1) Start system.
2) Recover password.
3) Enter command shell.
 
Option? 3
Password:
=> help
 
=> printenv
AutoLoad=yes
BootromVerbose=no
InitTest=MEM()
LoadIdentifiers=Fabric Operating System;Fabric Operating System
OSLoadOptions=quiet;quiet
OSLoader=ATA()0x94f98;ATA()0xa317
OSRootPartition=hda2;hda1
SkipWatchdog=yes
baudrate=9600
bootcmd=setenv bootargs mem=${mem} ${OSLoadOptions};ataboot;bootm 0x400000
bootdelay=20
ethact=ppc_4xx_eth0
ethaddr=00:05:33:4A:76:82
gatewayip=192.168.16.1
hostname=sequoia
initrd_high=0x20000000
ipaddr=192.168.16.43
mem=520192k
preboot=echo;echo Type "run flash_nfs" to mount root filesystem over NFS;echo
netdev=eth0
consoledev=ttyS1
ramdiskaddr=400000
ramdiskfile=your.ramdisk.u-boot
stderr=serial
stdin=serial
stdout=serial
submask=255.255.255.0
ver=U-Boot 1.1.3 (Mar 31 2011 - 12:16:18)
=> setenv AutoLoad no
=> setenv BootromVerbose yes
=> setenv hostname
=> setenv ipaddr
=> setenv gatewayip
=> setenv submask
=> setenv OSLoadOptions
=> setenv SkipWatchdog no
=> setenv bootcmd 'setenv bootargs single mem=${mem} ${OSLoadOptions};ataboot;bootm 0x400000'
=> saveenv
Saving Environment to Flash...
 
. done
 
. done
done
```
5. remove the flash memory module and set it to the side
6. now boot her up and you should have root
```
=> boot
ATA device vendor SILICONSYSTEMS INC 512MB-3625, product CB34526481500B150W00, revision 241-0230
Map file at LBA sector 0x94f98
Number of fragments is 0x3
End dest point is 0x00813000.
## Booting image at 00400000 ...
   Image Name:   Linux-2.6.14.2
   Image Type:   PowerPC Linux Multi-File Image (uncompressed)
   Data Size:    4269595 Bytes =  4.1 MB
   Load Address: 00000000
   Entry Point:  00000000
   Contents:
   Image 0:  3190918 Bytes =  3 MB
   Image 1:  1078663 Bytes =  1 MB
## Current stack ends at 0x1FAEFA68 => set upper limit to 0x00C00000
## initrd at 0x0070B0D4 ... 0x0081265A (len=1078663=0x107587)
   Loading Ramdisk to 1f9e7000, end 1faee587 ... OK
initrd_start = 1f9e7000, initrd_end = 1faee587
## Transferring control to Linux (at address 00000000) ...
mmu_mapin_ram pins 2 tlb
Linux version 2.6.14.2 (swrel@hq1-ub-ecbld-105) (gcc version 3.4.6) #1 Thu Mar 31 12:10:40 PDT 2011
Silkworm CPLD [board: 75, rev: 2]
Brocade Silkworm port (C) 2007 DENX Software Engineering (sr@denx.de)
  DMA zone: 130048 pages, LIFO batch:31
  Normal zone: 0 pages, LIFO batch:1
  HighMem zone: 0 pages, LIFO batch:1
Built 1 zonelists
Kernel command line: single init=/bin/bash mem=520192k
PID hash table entries: 2048 (order: 11, 32768 bytes)
Dentry cache hash table entries: 65536 (order: 6, 262144 bytes)
Inode-cache hash table entries: 32768 (order: 5, 131072 bytes)
Memory: 503040k available (2380k kernel code, 772k data, 128k init, 0k highmem)
Mount-cache hash table entries: 512
checking if image is initramfs...it isn't (no cpio magic); looks like an initrd
Freeing initrd memory: 1053k freed
NET: Registered protocol family 16
PCI: Probing PCI hardware
SCSI subsystem initialized
Initializing Cryptographic API
IBM gpio driver version 06.12.06
SWBD Platform Driver v1.0: [type 75, rev 2].
Config Silkworm
PPC 405 watchdog driver v0.51. (Timer driven)
Serial: 8250/16550 driver $Revision: 1.90 $ 4 ports, IRQ sharing enabled
ttyS0 at MMIO 0x0 (irq = 1) is a 16550A
ttyS1 at MMIO 0x0 (irq = 0) is a 16550A
ttyS2 at MMIO 0x0 (irq = 35) is a 16550A
ttyS3 at MMIO 0x0 (irq = 36) is a 16550A
io scheduler noop registered
io scheduler anticipatory registered
io scheduler deadline registered
io scheduler cfq registered
RAMDISK driver initialized: 1 RAM disks of 50000K size 1024 blocksize
loop: loaded (max 8 devices)
PPC 4xx OCP EMAC driver, version 3.54
mal0: initialized, 2 TX channels, 2 RX channels
rgmii0: input 0 in GMII mode
eth0: emac0, MAC 00:05:33:4a:76:82
eth0: found BCM5421 PHY (0x01)
tun: Universal TUN/TAP device driver, 1.6
tun: (C) 1999-2004 Max Krasnyansky <maxk@qualcomm.com>
Uniform Multi-Platform E-IDE driver Revision: 7.00alpha2
ide: Assuming 33MHz system bus speed for PIO modes; override with idebus=xx
<7>Probing IDE interface ide0...
hda: SILICONSYSTEMS INC 512MB-3625, ATA DISK drive
ide0 at 0xe301e3e0-0xe301e3e7,0xe301e7ec on irq 64
hda: max request size: 128KiB
hda: 1019088 sectors (521 MB) w/0KiB Cache, CHS=1011/16/63
hda: cache flushes not supported
hda: hda1 hda2
ATA polled-mode panic dumper on char-major-252.
mtdchar: write-caching enabled
silkworm: Using SWBD34 flash configuration
Boot flash: Found 1 x16 devices at 0x0 in 16-bit bank
Intel/Sharp Extended Query Table at 0x0031
Using buffer write method
cfi_cmdset_0001: Erase suspend on write enabled
Creating 6 MTD partitions on "Boot flash":
0x00000000-0x00020000 : "bootenv0: boot environment (1)"
0x00020000-0x00040000 : "bootenv1: boot environment (2)"
0x00040000-0x00200000 : "prom0: boot prom (1)"
0x00200000-0x003c0000 : "prom1: boot prom (2)"
0x003c0000-0x003e0000 : "unused"
0x003e0000-0x00400000 : "bootsel: boot prom selector"
i2c /dev entries driver
IBM IIC driver v2.1
ibm-iic0: using standard (100 kHz) mode
ibm-iic1: using standard (100 kHz) mode
iic1: Registered I2C mux callback for SWBD75
M41T11 Real-time-clock Driver v1.1
m41t11: Called to probe for bus IIC-0
m41t11: I2C Real-Time-Clock detected on iic0 addr 0x68
NET: Registered protocol family 2
IP route cache hash table entries: 4096 (order: 2, 16384 bytes)
TCP established hash table entries: 16384 (order: 4, 65536 bytes)
TCP bind hash table entries: 16384 (order: 4, 65536 bytes)
TCP: Hash tables configured (established 16384 bind 16384)
TCP reno registered
ip_tables: (C) 2000-2002 Netfilter core team
TCP bic registered
Initializing IPsec netlink socket
NET: Registered protocol family 1
NET: Registered protocol family 10
IPv6 over IPv4 tunneling driver
ip6_tables: (C) 2000-2002 Netfilter core team
NET: Registered protocol family 17
NET: Registered protocol family 15
RAMDISK: Compressed image found at block 0
EXT2-fs warning: mounting unchecked fs, running e2fsck is recommended
VFS: Mounted root (ext2 filesystem).
Installing Linuxxfsshutdownhandler_module: module license 'unspecified' taints kernel.
2.6 Kernel
Attempting to find a root file system on hda2...
kjournald starting.  Commit interval 5 seconds
EXT3 FS on hda2, internal journal
EXT3-fs: recovery complete.
EXT3-fs: mounted filesystem with ordered data mode.
kjournald starting.  Commit interval 5 seconds
EXT3-fs: mounted filesystem with ordered data mode.
VFS: Mounted root (ext3 filesystem) readonly.
Trying to move old root to /initrd ... okay
Freeing unused kernel memory: 128k init
```
7. Now the passwd bin is messed up and there are very few utilities, I basically ended up using openssl (hahahahaahah yes I misused the crap out of openssl but she does do md5…) to generate a password for me and then just echoed the thing back in because sed / awk vim was borked.
 
```
sh-2.04# passwd root
passwd: User not known to the underlying authentication module
sh-2.04# passwd user
passwd: User not known to the underlying authentication module
sh-2.04# /fabos/bin/passwd root
fabosShowInit failed: -1
sh-2.04# /fabos/bin/passwdDefault
fabosShowInit failed: -1
sh-2.04# which makepasswd
which: no makepasswd in (/usr/local/sbin:/sbin:/bin:/usr/sbin:/usr/bin)
sh-2.04# which openssl
/usr/bin/openssl
sh-2.04#
openssl passwd -1 -salt ihatepasswordsandstufftody200b1c0805b1328da450070c8486a863 fibranne
sed -i.bak s#$1$ic1kUR30$bLUYJoPuCJeOqNTfuO4x11#$1$ihatepas$XusucOp8N/IriZrD12hTE/#g /etc/shadow.test
cat > /etc/shadow <<EOL
root:\$1\$ihatepas\$XusucOp8N/IriZrD12hTE/:15398::::::
factory:\$1\$dTY4MrdH\$I/ZaVPK6frNo0sa/1Xsxe0:15398::::::
admin:4/WzpaAcD4IXw:15398::::::
user:\$1\$gUX5viE1\$y1KU/OUr/duXFUEqkSPmS.:15398::::::
EOL
3cat > /etc/passwd <<EOL
root:\$1\$ihatepas\$XusucOp8N/IriZrD12hTE/:0:0:root:/root:/bin/sh
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:
adm:*:3:4:adm:/var/adm:
lp:*:4:7:lp:/var/spool/lpd:
sync:*:5:0:sync:/sbin:/bin/sync
shutdown:*:6:0:shutdown:/sbin:/sbin/shutdown
halt:*:7:0:halt:/sbin:/sbin/halt
mail:*:8:12:mail:/var/spool/mail:
news:*:9:13:news:/var/spool/news:
uucp:*:10:14:uucp:/var/spool/uucp:
ftp:*:14:50:FTP User:/export/local/ftp:/
nobody:*:99:99:Nobody:/:
switchadmin:*:0:604:SwitchAdmin:/fabos/users/switchadmin:/bin/rbash
operator:*:0:605:Operator:/fabos/users/user:/bin/rbash
zoneadmin:*:0:606:ZoneAdmin:/fabos/users/user:/bin/rbash
fabricadmin:*:0:607:FabricAdmin:/fabos/users/user:/bin/rbash
basicswitchadmin:*:0:608:BasicSwitchAdmin:/fabos/users/user:/bin/rbash
securityadmin:*:0:609:SecurityAdmin:/fabos/users/user:/bin/rbash
factory:\$1\$dTY4MrdH\$I/ZaVPK6frNo0sa/1Xsxe0:0:601:Diagnostics:/fabos/users/diag:/bin/rbash
admin:\$1\$RJrV9hXJ\$sS..xZx12tH9TL5zOCGjb0:0:600:Administrator:/fabos/users/admin:/bin/rbash
user:\$1\$gUX5viE1\$y1KU/OUr/duXFUEqkSPmS.:0:602:User:/fabos/users/user:/bin/rbash
EOL
sh-2.04# reboot
```
8. Now after the changes, we need to reset things to normal
```
System RAM test using Default POST RAM Test succeeded.
 
set_bootstatus: BS_LOAD_OS, platform_idx = 5
 
Type run flash_nfs to mount root filesystem over NFS
 
Hit ESC to stop autoboot:  0
 
1) Start system.
2) Recover password.
3) Enter command shell.
 
Option? 3
Password:
=> printenv
AutoLoad=no
BootromVerbose=yes
DEFAULT_RUNLEVEL=1
InitTest=MEM()
LoadIdentifiers=Fabric Operating System;Fabric Operating System
OSLoader=ATA()0x94f98;ATA()0xa317
OSRootPartition=hda2;hda1
SkipWatchdog=no
baudrate=9600
bootcmd=setenv bootargs single mem=${mem} ${OSLoadOptions};ataboot;bootm 0x400000
bootdelay=20
ethact=ppc_4xx_eth0
ethaddr=00:05:33:4A:76:82
gatewayip=192.168.16.1
init=1
initrd_high=0x20000000
ipaddr=192.168.16.43
mem=520192k
preboot=echo;echo Type "run flash_nfs" to mount root filesystem over NFS;echo
netdev=eth0
consoledev=ttyS1
ramdiskaddr=400000
ramdiskfile=your.ramdisk.u-boot
setenv=test
stderr=serial
stdin=serial
stdout=serial
submask=255.255.255.0
ver=U-Boot 1.1.3 (Mar 31 2011 - 12:16:18)
 
Environment size: 799/4080 bytes
=> setenv AutoLoad yes
=> setenv BootromVerbose no
=> setenv hostname enc5-b2
=> setenv ipaddr 192.168.16.221
=> setenv gatewayip 192.168.16.1
=> setenv submask 255.255.255.0
=> setenv OSLoadOptions 'quiet;quiet'
=> setenv SkipWatchdog yes
=> setenv bootcmd 'setenv bootargs mem=${mem} ${OSLoadOptions};ataboot;bootm 0x400000'
=> saveenv
=> saveenv
Saving Environment to Flash...
 
. done
 
. done
done
=> boot
```
And now I can haz root

``` 
M5424-B1 console login: root
Password:
 
-----------------------------------------------------------------
Disclaimer for Root and Factory Accounts Usage!
 
This Fibre Channel switch is equipped with Root and Factory accounts
that are intended for diagnostics and debugging purposes solely by
the Equipment vendor's trained engineers. Improper use of the
functionality made available through the Root or Factory account could
cause significant harm and disruption to the operation of the SAN fabric.
 
Your use of the functionality made available through the Root or Factory
account is at your sole risk and you assume all liability resulting from
such use. The Equipment vendor shall have no liability for any losses
or damages arising from or relating to the use of the Root or Factory
account (and the functionality enabled thereby) by anyone other than
the Equipment vendor's authorized engineers.
 
Proceeding with the usage of this switch as the Root or Factory user
explicitly indicates your agreement to the terms of this disclaimer.
 
M5424-B1:root>
```
