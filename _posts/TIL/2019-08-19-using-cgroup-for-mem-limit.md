---
layout: post
title: Using cgroup for memory limitation
categories: TIL
tags: [commands, linux, memory, setting]
---
should be umount before rmdir or else will be a error message 
> Device or resource busy

```
MEMCG_ORIG_DIR=/sys/fs/cgroup/memory/
MEMCG_DIR=/sys/fs/cgroup/memory/test
sudo mkdir $MEMCG_DIR
sudo bash -c "echo $$ >> $MEMCG_DIR/cgroup.procs"
sudo bash -c "echo $MEMLIM > $MEMCG_DIR/memory.limit_in_bytes"
sudo rmdir $MEMCG_DIR
```
