---
layout: post
title: synchronization with levels
categories: GPU
---

# ![Cooperative Groups](http://on-demand.gputechconf.com/gtc/2017/presentation/s7622-Kyrylo-perelygin-robust-and-scalable-cuda.pdf)
A flexible model for synchronization and communication within groups of threads

> Before CUDA 9.0 '\_syncthreads()' was proposed for block level synchronization. But starting from CUDA 9.0, in order of bottom to top


|Level | Group | code|
|----|----|----|
|Thread|current coalesced set       | coalesced_threads();|
|Thread|warp-sized group            | tiled_partition<size>(block);|
|Block |CUDA Thread Block           | this_thread_block();|
|Grid  |device-spaning grid         | this_grid();|
|Grid  |Multiple grids spanning GPU | this_multi_grid();|

```
g = this_thread_block();  //thread launch
tiled_partition(g, 32);   // threds in thread_block
```
# reference
http://on-demand.gputechconf.com/gtc/2017/presentation/s7622-Kyrylo-perelygin-robust-and-scalable-cuda.pdf
