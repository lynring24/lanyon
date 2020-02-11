---
layout: post
title: Unified Memory in CUDA
categories: GPU
---
Unified Memory
Depends on which NVIDIA GPU archritecture one is using, but for after Pascal model 'unified memory' is supported.
Unified Memory is a single memory address apce accessible from any processor in a system. This hardware/software tech allows application to allocate data that can be read or written from code running on either CPU/GPU.

```
cudaError_t cudaMallocManaged(void** prt, size_t size);
```
cdoe running on a CPU/GPU access data allcoated, the CUDA system software and/or the hardware takes care of migrating  memory pages to the memory  of the accessing processor. The Pascal GPU archritecture is the first with hardware support for virtual memory page faulting and migration, via its Page Migration Engine. Older GPU based on the Kepler  and Maxwell architecutres also support a more limited form of Unified Memory.

## Unified Memory in Kepler
Tesla K80과 같은 pre-Pascal GPU에서는 cudaMallocManaged()를 호출하면 GPU device에 size만큼 메모리를 할당하게 된다. Driver는 page table entry를 관리하며 모든 page할당에 대한 정보를 갖고 있도록 한다.
**DEEP COPY** CUDA runtime must migrate all pages previously migrated to host memory or to another GPU back to the device memory.

```
__host__​cudaError_t cudaMemPrefetchAsync ( const void* devPtr, size_t count, int  dstDevice, cudaStream_t stream = 0 )
Prefetches memory to the specified destination device.
```

Deep copy 시에는 src와dest가 모든 page 데이터를 각자 들고 있어야한다는 문제가 있다.
unified memory를 사용하면 어떤 processsor인지 상관없이(?) 메모리를 공유해서 하나의 virtual address를 사용하게 된다.

## Unified Memory in After Pascal Architectures
Memory allcoation is not physically done with cudaMallocManaged(). Rather it is allocated and set when they are accessed by the GPU or CPU. The pages can migrate to any processor memory at any time and driver employs heuristics to maintain data locality and prevent execessive page faults.



### Reference
![Everythig needed to know 'bout unified-memory] (http://on-demand.gputechconf.com/gtc/2018/presentation/s8430-everything-you-need-to-know-about-unified-memory.pdf)
![Unified memory cuda beginners](https://devblogs.nvidia.com/unified-memory-cuda-beginners)
