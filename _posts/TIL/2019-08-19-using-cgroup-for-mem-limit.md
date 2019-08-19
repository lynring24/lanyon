
---
layout: post
title: Using cgroup for memory limitation
categories: TIL
---

```
MEMCG_ORIG_DIR=/sys/fs/cgroup/memory/
MEMCG_DIR=/sys/fs/cgroup/memory/run_mem_lim_$USER
sudo mkdir $MEMCG_DIR
sudo bash -c "echo $$ >> $MEMCG_DIR/cgroup.procs"
sudo bash -c "echo $MEMLIM > $MEMCG_DIR/memory.limit_in_bytes"
sudo rmdir $MEMCG_DIR
```
