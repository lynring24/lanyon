---
layout: post
title: Unified Memory in CUDA 1
categories: GPU
---

# Unified Memory
Depends on which NVIDIA GPU archritecture one is using, but for after Pascal model 'unified memory' is supported.
Unified Memory is a single memory address apce accessible from any processor in a system. This hardware/software tech allows application to allocate data that can be read or written from code running on either CPU/GPU.

```
cudaError_t cudaMallocManaged(void** prt, size_t size);
```
cdoe running on a CPU/GPU access data allcoated, the CUDA system software and/or the hardware takes care of migrating  memory pages to the memory  of the accessing processor. The Pascal GPU archritecture is the first with hardware support for virtual memory page faulting and migration, via its Page Migration Engine. Older GPU based on the Kepler  and Maxwell architecutres also support a more limited form of Unified Memory.

### Characteristic
1. Simpler Programmin & Memory model
- single pointer to data
- simpler Interface
2. Performance through data locality
- migrate data to accessing processor
- Guarantee global coherency
- allows cudaMemcpyAsync()


## Unified Memory in Pre-Pascals
Tesla K80과 같은 pre-Pascal GPU에서는 cudaMallocManaged()를 호출하면 GPU device에 size만큼 메모리를 할당하게 된다. Driver는 page table entry를 관리하며 모든 page할당에 대한 정보를 갖고 있도록 한다.
**DEEP COPY** CUDA runtime must migrate all pages previously migrated to host memory or to another GPU back to the device memory.

```
__host__​ cudaError_t cudaMemPrefetchAsync (
                         const void* devPtr,
                         size_t count,
                         int  dstDevice,
                         cudaStream_t stream = 0 )
// Prefetches memory to the specified destination device.
```

Deep copy 시에는 src와 dest가 모든 page 데이터를 각자 들고 있어야한다는 문제가 있다. Unified memory를 사용하면 어떤 processsor인지 상관없이(?) 메모리를 공유해서 하나의 virtual address를 사용하게 된다.
Pre-Pascal GPU 모델들은 해당 architecture는 page-fault별도로 처리하지 않는다. Device 정보 중 **concurrentManagedAccess()** 는 해당 GPU가 HW page migration과 concurrent access의 가능 여부를 알려준다 (return 값이 1인 경우).
(물론 **cudaStreamAttachMemAsync()** 처럼 allocation시점을 직접 처리할 수 있긴하지만, default로는 stream에 allocation을 묶어서 처리한다.)

> No GPU page fault support: move all dirty pages on kernel launch

> No concurrent access, no GPU memory oversubscribption, no system-wide atomics

## Unified Memory in After Pascal Architectures
Memory allcoation is not physically done with cudaMallocManaged(). Rather it is allocated and set when they are accessed by the GPU or CPU. The pages can migrate to any processor memory at any time and driver employs heuristics to maintain data locality and prevent execessive page faults. **cudaMemAdvise()** 로 사용자는 추천을 받거나,  **cudaMemPrefetchAsync()** 를 사용해서 직접 설정할 수 있다.
> Supporting page fault and migration is the biggest difference

Kernel 수행 전에 host->device 또는 device->device로 page copy가 발생하는데, Pascal부터는 이 작업을 runtime에 진행하지 않는다. Kernel은 data migration overhead 없이 이동하며 page에 access를 할 때 부재한다면 GPU는 대기하고 Page Migration Engine이 migrate 해줄 때까지 기다린다. Runtime에 data migration이 발생하므로 kernel execution만 고려한다면 pre-Pascal과 비교했을 때 수행 시간이 더 걸린다.

### Runtime data migration overhead
실제 appliction에서 GPU가 CPU와 통신을 할 일이 많은가를 생각해본다면, CPU가 data를 초기화해서 GPU로 이동시키는 경우 한번 밖에 없다. 대개 한번 이동시킨 데이터를 가지고 GPU는 별다른 개입없이 연산을 하게된다. 이런 overhead를 줄일 방법은
1. 아예 kernel내에서 데이터를 initialize한다.
2. (성능을 재는 경우) 여러 번 수행시켜서 평균이나 최소 runtime을 고려한다.
3. Data를 kernel launch 전에 prefetch해서 사용한다.

### Consider the Unified Memory on Pascal and Later GPUs
Pascal GPU architecure부터는 49-bit virutal address와 on-demand page migration를 지원한다. 32 bit가 아니라 49 bit로, 전체 시스템 메모리 (흔히 알고 있는 메인 메모리)와 모든 GPU의 메모리를 접근가능하게 만들었다. CPU, GPU가 동시에 접근 할 수 있다는 전제하에 **cudaDeviceSynchronize()** 를 둬서 segmentation fault를 방지하도록한다. Page fault를 지원한다는 이야기는 memory oversubscribing이 가능하다는 이야기로, 여러 GPU를 돌릴떄 application을 수정하게 되는 수고를 줄인다.

Pascal과 Volta에서 system-wide atomic memory operation을 지원하는 점을 고려해볼 때, 여러 GPU에서 atomic 연산을 처리할 수 있는데 multi-GPU cooperative algorithm을 작성할 때 유리하다.

Demand paging은 sparse pattern data, 즉 어떤 메모리 address가 어떤 특정 processor에 접근할지 모르는 경우 유리하다. Page fault를 지원하진 않으면 application은 일단 전체 데이터를 다 올려서 처리해야하는데, 지원을 한다면 굳이 다 올릴 필요가 없다.

### GPU Page Table
+ CPU page table과 별도로 운영되  GPU memory에 위치한다.
+ Physical address는 GPU channel descriptor에 있다.
+ 모든 command와 program은 channel를 통해 가상 주소로 처리되는데 GPU page table은 GPU virtual address를 GPU device physical address뿐만 아니라 host physical address까지 변환한다.

## Reference
- [Everythig needed to know 'bout unified-memory](http://on-demand.gputechconf.com/gtc/2018/presentation/s8430-everything-you-need-to-know-about-unified-memory.pdf)
- [Unified memory cuda beginners](https://devblogs.nvidia.com/unified-memory-cuda-beginners)
- [Beyond GPU Memory Limits with Unified Memoery on Pascal](https://devblogs.nvidia.com/beyond-gpu-memory-limits-unified-memory-pascal/)
- [GPU architecture overhead](https://insujang.github.io/2017-04-27/gpu-architecture-overview/)
- [SC13-Unified-Memory-CUDA](http://on-demand.gputechconf.com/supercomputing/2013/presentation/SC3120-Unified-Memory-CUDA-6.0.pdf)
