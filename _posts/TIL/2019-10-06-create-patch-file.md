---
layout: post
title: create patch file 
categories: TIL
---

### patch file from two different directories
```
diff -ur TARGET_DIR SOURCE_DIR > patch.diff
patch -i patch.diff
```
