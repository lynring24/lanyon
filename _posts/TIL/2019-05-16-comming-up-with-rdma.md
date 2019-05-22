---
layout: post
title:  Sipping RDMA
categories: TIL
---
## RDMA
RDMA, or as Remote Direct Memory Access is a technique to access the memory of remote device without bothering CPU. 
To make this come true there are special NIC card called RNIC (even NIC card is really unfamiliar for me.) 

```
The process is like below: 
RNIC of remote connects to RNIC of remote and access the memory.
The data flows into the host by RNIC
The RNIC of host pass the data to DMA of host and paste.  
```

![sw](../images/RMDA.PNG)

<pre>
There are two types of RDMA: one-sided and two-sided.
What mostly known is one-sided RMDA which uses only the host CPU but not the remote CPU.
Two sided uses the CPU of both side.
</pre>