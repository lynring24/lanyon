---
layout: post
title: Verbs in RDMA
categories: TIL
---
### Verbs
Verbs is an abstract (but a low level) description of the functionality that is provided for applications for using RDMA.
Same API is used for all RDMA-enabled transport protocols.

#### Two major Groups of Verbs
Control Path - manage the resources and usually requires context switch 
Data Path - use the resources to send/receive data and doesn’t require context switch.

> from the ![document](https://www.csm.ornl.gov/workshops/openshmem2014/documents/presentations_and_tutorials/Tutorials/Verbs%20programming%20tutorial-final.pdf)
