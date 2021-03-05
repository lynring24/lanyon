---
layout: post
title: change file extension 
categories: TIL
tags: [command, linux]
---

To change or make a copy of existing files, 
```
$ find . -name '*.yml.sample' -exec sh -c 'cp "$0" "${0%.sample}"' {} \; 

# find the files suits in regex
# run shell to copy the files
# get string ${0%.sample}
```
