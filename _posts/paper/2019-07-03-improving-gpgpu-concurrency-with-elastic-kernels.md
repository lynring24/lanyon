---
layout: post
title: Improving GPGPU Concurrency with Elastic Kernels
categories: paper
---

### 글쓴이
+ Sreepathi Pai, Matthe J.Thazhuthaveetil, R. Govindarajan 
+ Supercomputer Eduaction and Research Centre, Indial Insitute of Science

### Abstract
GPU concurrency를 높이기 위해 kernel을 변형한다.  한 grid당 수행 가능 자원에 대한 제한이 있다보니 자원이 있더라도 실행되지 않는 경우가 있다. 하드웨어 단에서 최적화하면 가장 효율이 좋겠지만, grid는 program model level 개념이기 때문에 불가능하다. 그렇다고 현재 돌고 있는 grid의 자원에 대한 정보를 바로 얻을 수 있는 것은 아니라서 다른 실행 중인 다른 grid나 실행 중인 grid 내의 stream을 참고해서 간접적으로 정보를 얻어야 한다. 논문에서 제시하는 Elastic Kernel은 CUDA의 wrapper로 runtime에 자원의 할당을 관리하며 기존의 LEFTOVER 정책보다 작은 단위(범위)의 concurrency를 구현했다.

### GPU Concurrency 
Stream은 GPU에 있어서 명령어 수행 단위로 연산을 주로하는 kernel stream과 memory 관리를 하는 memory stream으로 나뉜다. DMA engine은 개수와 concurrency가 비례하지만, memory 쪽에 bottleneck이 생긴다는 점에서 무작정 수를 늘릴 수 없다. Thread block scheduler은 사용자가 지정한 커널에 대한 grid를 인스턴스화하고, thread block들을 SM에 보낸다. 

#### Serialize due to lack of resources
**LEFTOVER** 독립적인 다른 grid들이 수행하고 있을 때 사용하지 않는 남은 자원들을 가지고 수행한다. 이를 "LEFTOVER" 정책이라고 하는데 concurrency를 늘 보장해주 않는다. Concurrency에 있어서 thread block이 1개라도 여유가 있었다면 새로운 grid를 수행할 수 있지만 그렇다고 독립적인 grid들이 언제나 동시에 실행됨을 보장하지는 않는다. LEFTOVER 정책의 대안으로 spatial partitioning 정책이 있다. 수행하는 grid의 thread block 단위로 SM(Streaming Multiprocessor)들을 할당한다. 

여러 grid가 같은 SM을 공유할 수 있다. Grid와 thread block의 차원을 수정해서 공유하는 방식이다. 

#### Serialization due to kernel Execution
kernel을 time slice 단위로 수행해서 concurrency를 높인다. GPU는 preemption이 불가능하므로 돌고 있는 kernel을 강제로 끄집어 낼 수 없다. Kernel의 state등을 고려했을 때 thread block scheduler가 스케줄 관리를 하기 위해 종료된 커널을 내리고 새로운 작업을 배치하는 시점을 wndeks point로 사용한다. 

### Elastic kernel
Elatic kernel은 프로그래머들이 요청한 logical grid N개와 physical grid 1개를 mapping한다. 이를 위해 kernel의  lock_per_grid와 thread_per_block도 조정한다. N개의 logical grid을 관리하려면 역으로 1차원 grid에서 다차원을 유도하게 된다. 
```
physical에서 logical id를 뽑아낼 때 


tid = physical 기준 global thread id
크기 = thread 개수 

for ( global_tid = tid; 현재 tid 부터 tid + 사용자가 요청한 grid 크기 만큼 ; physical grid 크기 ) {

	// global_tid를 logical block per grid로 나눠서 logical block id와 logical thread id를 계산한다. 
	block_id = global_tid / logical block per grid 
	thread_id = gloabal_tid % logical block per grid 

	// logical block id에서 logical grid dimesion의 차원을 구하고, 

	// logical thread id에서 logical block dimension의 x, y, z에 대한 값을 구한다. 

}

```

#### Kernel의 잉여 자원 관리
Kernel의 잉여 자원을 관리하기 위해서 현재 사용하고 있는 SM에 대한 정보들과 limit을 비교해서 최소한의 자원을 가지고 수행하도록 맞춘다. 
