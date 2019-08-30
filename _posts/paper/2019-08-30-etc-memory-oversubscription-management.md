---
layout: post
title: ETC,  A Framework for Memory Oversubscription Management in Graphics Processing Units
categories: paper
---

## Abstract
Memory oversubscription시에 GPU page eviction latency, thrashing  cost, 메모리 사용률 등을 해결하기 위한 memory management framework. Application의 타입과 메모리 공유 여부에 따라 적절한 memory management 기법을 사용한다.
```
IF ( GPU의 physical 메모리 > 할당된 전체 메모리) {
  check_and_classify (Compile-time 정보, HW 정보)  
  IF (규칙적인 application) {
      gpu driver의 virtual memory manager의 proactive eviction 실행.
	    IF (sharing data)
      	 memory compression 실행.  
  } ELSE /* 불규칙적인 application*/
      memory-aware throttle + memory compression
}
```

## Application Classification
ETC가 어떤 application에게 어떤 기법을 쓸지를 정할 때  1) 각 SM에 돌아가는 application의 타입과 2) kernel간에 공유하는 메모리의 양을 고려한다.

#### 프로그램의 종류
Memory coalescing 통계를 사용 (같은 warp에서 같은 cache을 요청할 때, memory coalescing unit은 중복을 줄이기 위해 두 요청을 합친다.) ETC은 각 SM의 load/store를 계산하여 coalesced 여부를 확인
```
If ( count > threshold )
    regular application
ELSE
    irregular application
```
#### Data 공유 여부 탐지
Compile-time information을 사용.
Compiler가 비슷한 pointer를 접근하면 application이 shared data를 사용한다고 판단. 

## Proactive Eviction
기존에는 page fault 후에 page eviction이 실행. Dual DMA engine 의 지원으로 fault로 인한 data migration과 eviction으로 인한 data migration의 중첩이 가능GPU driver을 수정해서 실제 application의 가용 memory가 없어지기 전에 page를 evict한다.
<pre>
2가지의 디자인 이슈 
1 )evict하는 시점	 
2) evict하는 page 양
</pre>

> 너무 이른 경우 -> GPU memory의 재사용이 어렵다.    
> 너무 늦은 경우 -> 이점인 latency를 줄어든다.

#### Avoiding Early Eviction
각 application을 profilingCPU->GPU 의 data migration 횟수(footprint) 를 시간 별로 정리, 증가 추이를 확인.  
<pre>
실험을 통해 결과 4가지
- 시간과 비례하여 증가한다. 
- ATAX의 경우 계단식 단계별로 증가하지만 여전히 비례하여 증가한다. 
- SIMT execution 모델은 같은 instruction을 다른 warp로 하여금 다른 데이터로 실행 모든 warp들이 병렬처리하고 global memory를 공유, 모든 데이터가 각 단계에서 fetch할 때 까지 증가한다. 
- page fault가 일어나는 시간차가 꽤나 일정하다. 
</pre>

>  GPU는 일정한 시간 동안 연속적으로 page fault가 일어날 수 있고 첫 page fault가 발생하자마자 여러 page eviction을 수행하게 된다. 

#### Avoiding Late Eviction 
**D-to-H의 data transfer 속도 >  H-to-D의 data transfer 속도**
H->D와 D->H의 data transfer을 동시에 수행함으로써 late eviction을 해결.
GPU driver가  proactive eviction의 실행 시간을 결정한다. (기준 : H->D와 D->H의 data transfer latency) Irregular application은 같은 시간 프레임 내에 여러 page들을 접근하기 때문에  proactive eviction이 비효율적이다. 

#### Implementation 
GPU runtime 내부에 virtual memory manager을 수정해서 새로운 proactive eviction unit을 생성
```
IF (page fault) {
  PEU는 GPU driver를 interrupt
  GPU driver가 fault된 page를 GPU 메모리로 이동
}
```
성공적으로 page를 할당하면 PEU는 Application Classification Logic을 사용해서 application에 대한 정보를 확인. 메모리 할당 크기와 가용 메모리 크기를 비교해서 oversubscribed 여부를 예측한다.

<pre>
PEU가 page evict하는 경우
 1)새롭게 할당해야하는 사이즈가 가용 GPU 메모리보다 클 경우
 2) GPU 메모리가 이미 over subscripted된 경우
 3) 가용 메모리사이즈가 threshold보다 작은 경우
</pre>

## Memory-Aware Throttling 
**문제**  Page-level thrashing은 irregular GPGPU application의 성능을 저하

<pre>
Thread의 수를 제한하는 데 2가지 방법
+ Thread Block throttling ( 각 SM의  thread block 일부만 사용)
+ SM을 throttling ( 각 GPU의 SM 일부의 사용 )

</pre>

#### Implementation
실험 시 TB throttling보다는 SM throttling이 보다 적용하기 쉬워서 ETC는 SM의 수를 제한하는 방법을 사용한다. Irregular application이고, memory가 oversubscribed 되었을 때 SM throttling을 실행한다.  ½ SM 새로운 instruction을 fetch하지 않도록 하고 점차 조정.
page fault가 발생했거나 탐지 시간이 종료된다면 탐지 단계를 종료한다. 이후, page fault 여부와 page eviction 여부 등을 고려해서 SM 을 결정한다. 
```
if (시간 종료 ) {
  working set이 GPU memor에 알맞게 들어갔다.
  Page thrashing 없이 더 많은 thread를 동시 실행이 가능하다 .
  SM을 따로 제한하지 않는다. 
}
else if ( page fault && ! page eviction )
     GPU 에 메모리 여유가 있다.

else if ( page fault  && 단 한번이라도 eviction ) {
     working set 크기가 메모리에 맞지 않다.
     SM이 메모리에 없는 page를 접근할 수 있으니, SM을 제한해서 working set size를 조절해야 한다.
  }
```
물론 thread-level 병렬을 제한하지만, 많은 data migration을 줄일 수 있고 memory oversubscription으로 인한 performance를 해결할 수 있다. 
Thread-level 병렬에 대한 부분은 memory-aware throttling을 capacity compression technique와 함께 적용함으로 해결할 수 있다. 

## Capacity Compression
**문제**
+ proactive eviction :  latency만 해결했을 뿐, page migration의 횟수는  줄이지 않는다. 
+ memory-aware throttling  :  thread-level parallel ↓

**해결책**
memory oversubscription의 비용을 줄이기 위해 압축한다. ()성능이 좋아질 것 같은 경우) 선택적으로 압축. 논문의 경우는 cpu시스템에서 효과를 본 linearly compressed pages 를 적용했다. 압축을 함으로 더 많은 데이터를 올릴 수 있다. 더불어 memory-aware throttling은 thread-level 동시 실행이 throttling만 사용했을 때 비해 더 수월하다.

#### Implementation
이미 memory controller와 PCIe bus를 통한 memory bandwidth compression이 가능하기 때문에 memory controller와 DMA unit은 하드웨어가 갖춰져 있다.추가로 512 entry metadata 캐시를 memory controller 안에 둔다.
