---
layout: post
title: Volta Unified Memory
categories: GPU
---

## Unified memory
On-demand migration to access processor on first touch

### Access Counter  (From Volta + Power9)
If the memory is mapped to the GPU, migration can be triggered by access counters
With access counters only hoy pages will be move to the GPU.
Migration are delayed compared to the fault-based method.

### Hardware coherency with NVLINK2
CPU can directly access adn cache GPU memory.
Native atomics support for all accessible memory.

### ATS Support (Volta + P9)
ATS, address translation service, supports CPU and GPU to share a single page table.

### Unified Memory with System Allocator
System allocator support allows GPU to access all system memory (malloc, stack, global, file system). P9, Address Translation Service(ATS) enabled in CUDA 9.2.
The initial version of patchset is integrated into 4.14 kernel. NVIDIA is planning to support the upcomming versions of HMM.

## Pages in aspect of CUDA Driver
GPU architecure supports different page sizes. Contiguous pages up to a large page size are promoted to the larger size. Driver prefetches whole regions if pages are accessed densely.

### Page Fault Group
한 개의 GPU page를 n개의 warp가 access할 때 기존에는 한 warp에서 fault가 발생하면 인근 warp도 함께 stall하다가 다시 replay하는 시점까지의 시간 'fault processing' 시간이었다.  

## System Wide atomics
[continue]
