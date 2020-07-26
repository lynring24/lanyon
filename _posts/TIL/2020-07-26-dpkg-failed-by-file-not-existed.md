---
layout: post
title: dpkg failure : file not existed
categories: TIL
---

```
# try
apt-get clean
apt-get install -fy
dpkg -i /var/cache/apt/archives/*.deb
dpkg --configure -a
apt-get install -fy
apt-get dist-upgrade

# if does not work 

sudo mkdir -p /var/lib/dpkg/{updates,alternatives,info,parts,triggers}
sudo killall apt* software-center* dpkg
sudo apt-get update
sudo apt-get purge wine1.4 ia32-libs-multiarch
sudo apt-get upgrade
```
