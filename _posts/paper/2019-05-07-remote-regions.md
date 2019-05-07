---
layout: post
title:  Remote regions: a simple abstraction for remote memory, USENIX
categories: paper
---
> this will be a jot down note for my understanding of the paper. 

#### Index
- Introduction And Goals
- Region Abstraction

## Introduction And Goals
Region system provides an simpler verbs interface of remote system, where the memory systems are operated by **files**. Two benchmarks have been used: R and metis. Since it is hard to use existing remoete meroy system, by using region jobs could be more simple.
> RDMA : remtoe memory interface  
> REGIONS : file interface

#### Comparsion with RDMA
+ interface : file, high-level
+ RDMA limits on memory registration, connection and keys.

#### Goals
providing abstractions for applications to access the memory of other applications across the network.

## Region Abstraction
> **owner** : creates a regions and operate tasks

#### Memory allocation
applications can dynamically allocate/free buffers within a region. T(rmalloc) < T(new_region)


