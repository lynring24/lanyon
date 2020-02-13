---
layout: post
title: SM and the Block
categories: GPU
---

A block in CUDA always executes on a single SM.

The Compute Work Distributor will schedule a thread block (CTA) on a SM only if the SM has sufficient resources for the thread block (shared memory, warps, registers, barriers, ...). Thread block level resources such shared memory are allocated.

MPS officially does not support dynamic programming and could see that to use hyper-q
(Anyway in Pre-Volta architecture)
After the jobs are launched, one that arrives lately will be queued in work dirstributer.

persistent thread only로 사용했을 때, dynamic programming을 고려하는 경우와는 다르게 host와의 data communication overhead를 무시할 수 없게 된다.

GPU SM 내부 자원
register file
shared memroy
...

CUDA Reduction
within warp thread execution이 많을 때, warp loop를 unroll해서 contention을 줄여본다.

Warped-Slicer
hardware-based, simulator로 돌렸고 처음으로 inter/intra SM concept를 제시하였다.
다양한 scheduling policy 중에서 봐둬야하는건 waterfilling 방식
-leftover policy
-even partitioning
-waterfilling algorithm : kernel들 중에서 가장 performance가 낮은 kernel에 대해 최소한의 자원을 할당해서 성능을 점차 (그나마 공평하게) 높이는 방법 => O(NK)
etc
intra/inter SM Slice 중에서 어떤 scheduler 정책을 사용할것인지 결정한다.
