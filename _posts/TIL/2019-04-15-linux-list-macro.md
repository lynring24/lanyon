---
layout: post
title:  list macro in C
categories: OS
tags: [os, kernel, system]
---
Interesting in C is that the link is implemented inside structure rather than the structure itself became a part of the list. 
Feels like each item is dangling on each node. 
Not used to macro functions in C, but found out they are handy to use. 

```
struct list_head {
  struct list_head *prev, *next;
}

struct task_head {
  pid_t pid;
  struct lsit_head list;
}

```
