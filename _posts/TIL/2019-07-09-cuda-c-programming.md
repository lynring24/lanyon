---
layout: post
title: cuda terms
categories: TIL
---

### Comute Capability 
SM version이라고도 하는데, 해당 GPU hardware에서 지원하는 feature에 대한 숫자 정보 
같은 version이라면 같은 core architecture를 갖는다. 볼타가 7, pascaldl 6 

### Context
CUDA의 context는 CPU의 process와 유사한 개념이다. Driver API가 수행하는 데 필요한 모든 자원과 연산에 대한 정보는 context에 담겨 있고, context가 종료되면 system은 즉시 자원들을 정리한다. module, texture, surface reference와 같은 공통 자원들을 제외하고 context는 개별적인 address space를 갖는다. 

### Stream 
Stream is a sequence of commands (possibly issued by different host threads) that execute in order.


