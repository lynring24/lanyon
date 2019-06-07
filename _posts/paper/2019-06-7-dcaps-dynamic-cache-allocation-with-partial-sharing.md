---
layout: post
title: DCAPS:Dynamic Cache Allocation with Partial Sharing
categories: paper
---

### Abstract
Dynamic Cache Allocation with Partial Sharing(DCAPS)은 multi-programmed workload의 cache demand를 동적으로 모니터하고 예측하는 프레임워크이다. 또한 cache partitioning에 있어서 partial sharing한다. 
DCAPS은 1)online MRC를 예측하기 위한 OPMRC, 2) CAT allocation하에 각 프로그램의 LLC occupancy를 측정하는 예측 모델 그리고 3) near-optiaml CAT scheme를 검색하기 위한 simulated annealing algorithm 이렇게 3 파트로 이뤄져 있다. 

#### Compare with KPart
DCAPS은 complete isolation, full share이 아닌 overlap을 통해 LLC를 사용하는 방식을 택했다.  KPart도 비슷한 방식으로 구현을 했었는데, Kpart은 MRC를 얻기 위해 online profiling을 사용한다. KPart의 MRC은 cache way에 따라 결정되는 반면 DCAPS는 모든 cache size를 다룰 수 있따. KPart는 IPC curve와 bandwidth curve utility에 유리하다.  

### OPMRC 
Online MRC는 실제 시스템에서 얻기 힘들다. OPMRC는 access trace를 참고해서 각 core에 대한 online LLC MRC를 얻는다. PEBS( Precise Event-Based Sampling)이라는 mechamism을 사용하는데, sampled된 loads와 stores의 address를 track한다. 이떄 동일  cache에 대해 reuse time이 reuse distance보다 게산하기 편하다는 점에서 average eviction time(AET)를 지표로 사용한다. Kernel에서 PEBS buffer와 outside buffer를 사용하게 되지만 user space에서는 따로 overhed가 발생하지 않는다. 실제 MRC와의 차이가 0.05정도 예측에 사용하기에는 정교한 편이다. 

### Optimal Cache allocation algorithm
Metrics로 Average MPKI, Throughput, Average sloadown, Fair slowdown , Maximum slowdown을 사용한다. 

