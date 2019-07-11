---
layout: post
title: cuda compilation
categories: TIL
---

Kernel들은 CUDA instruction set architecture, PTX, 를 사용해서 작성된다. NVCC copmiler driver는 C와 PTX 컴파일러를 단순화시켰다. 

### Compilation Workflow
compiling the device code into assembly form (PTX) and/or binary form (Cubin object). 다만 Cubin은 closed 되어있어서 역공학이 필요해서 OPBF라는 형식으로 대체하는 방식을 사요하기도 한다. 

#### Binary Capability 
Cubin object is generated using the compiler option -code: specified target architecture.
> -code = sm_35  # compute capability가 3.5이상안 device에서 binary code 실행이 가능하다. 

#### PTX Compatability 
** Warp shuffle funcions ** supported on devices of compute capability equal or above. when compiling from C to PTX. 
> -arch=compute_30 
> -rdc=true  	# create relocatbale device code
> -lcudadevrt 	# dyanmic parallelism supported by the device runtime library