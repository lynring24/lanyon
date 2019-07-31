---
layout: post
title:  No space left on device
categories: TIL
---

The partition with root and home directory was splitted in a quite odd way which made the device out of memory.  Mounting a device was not a option in this case. The memory was acually the logical volume not the physical. To get a new volume and add up was the job to do.

### check device and memory

> $ df -h

By checking the memory, the memory of server was out not in a faken way. There were some cases that usage was high though there are lots of available memory but was not this case.

> $ lsblk  

To check what devices are on line. Choose an available device  here.

### get disk partition

> $ fdisk /dev/sdX

With the  chosen device , make a disk partition. Mostly, this will work like : **/dev/sdX --> /dev/sdX#**. The X will be a device id and # will be the number of parition.

###  Physical volume
> $ pvcreate /dev/sdX#

Create a new physical volume with the assigned disk parition.

> $ pvdisplay

Check the physical volume list.

> $ vgcreate VOLUME_GROUP_NAME /dev/sdX# (/dev/sdX#)*  
> $ vgextend VOLUME_GROUP_NAME /dev/sdX# (/dev/sdX#)*
> $ vg remove VOLUME_GROUP_NAME

Create a volume group. To extend the existing volume group, use vgextend.

> $ lvcreate -n LOGICAL_VOLUME_NAME -l SIZE VOLUME_GROUP_NAME

### Logical group

Create a logical volume group.

> $ mkfs.ext4 /dev/sdX#

Format a file system to ext4.

> $ mount -t ext4 /dev/sdX# /SOME_DIRECTORY

Mount file system if needed.

### Nutshell
The jobs was to extend the volume so did not have to create a logical group but could be help to know.
