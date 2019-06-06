---
layout: post
title:  RDMA Architecture Abstract
categories: RDMA
---
> This document is based on http://www.mellanox.com/related-docs/prod_software/RDMA_Aware_Programming_user_manual.pdf 

## RDMA Architecture Abstract

### Infiniband
Infiniband(IB) is a server and storage interconnect technology supporting for native RDMA. Data transfer between server-server or server-storage w/o involvement of host CPU in the data path. Infiband uses I/O channels for data communication, where each channel provides the semantics of a virtualized NIC or HCA. InfiniBand uses copper and optical fiber connections. 

### Virtual Protocol Interconnect(VPI)
The Mellanox Virtual Protocol Interconnect architecture supports both InfiniBand and Ethernet semantics. A VPI adapter or switch can be set to deliver either InfiniBand or Ethernet sematics per port. A dual-port VPI adapter can be configured to one of the following options.

### RDMA over Converged Ethernet (RoCE)
RoCE is a standard for RDMA over Ethernet that is also defined and specified by the IBTA organization. RoCE provides true RDMA semantics for Ethernet as it does not require the complex and low performance TCP transport (needed for iWARP).
RoCE is the most efficient low latency Ethernet solution today. It requires a very low CPU overhead and takes advantage of Priority Flow Control in Data Center Bridging Ethernet for lossless connectivity. 


## Comparison of RMDA Technologies 
InfiniBand, Ethernet RoCE and Ethernet iWARP share a common user API which is defined in this document, but hace diffent physical and link layers. 
RDMA technologies are based on networking concepts found in a traditional network but there are differences that RDMA provieds a messaging service which applications can use to directly access the virtual memory on remote computers. The messaging service can be used for Inter Process Communicationm, communication with remote servers and to communicate with storage devices and to communicate with storage with storage devices using Upper Layer Protocols (ULP).
RDMA provides low latency through stack bypass and copy avoidance, reduces CPU utilization, reduces memory bandwidth bottlenecks and provides high bandwidth utilization. The key benefits that RDMA delivers accrue from the way that the RDMA messaging service is presented to the application and the underlying technologies used to transport and deliver those messages. RDMA provides Channel basedI/O. This channel allows an application using a RDMA device to directly read and write remote virtual memory.
In tranditional sockets networks, applications request network resources from the operating system through an API which conducts the transaction on their behalf. However RDMA use the OS to establish a channel and then allows applications to directly exchange message without further OS intervention. A message can be and RDMA Read, and RDMA Write operation or a Send/Recieve operation. IB and RoCE also support Multicast transmission.

The IB Link layer offers feature such as a credit based flow control mechanism for congestion control. It also allows the use of Virtual Lanes(VLs) which allow simplification of the higher layer level protocols and advanced Quality of Service. It guarantees strong ordering within the VL along a given path. The IB Transpot layer provides reliability and delivery guarantees. 

The Network Layer used by IB has features which make it simple to transport messages directly between applications' virtual memeory even if the applications are physically located on different servers. Thus the combination of IB Transport Layer with the Software Transport Interface is better thought of as a RDMA message transport service. 

## Key components 
#### HCA (Host Channel Adapter)
HCAs provide the point at which an IB end node connects to and IB network. These are the equivalent of the Ethernet card but HCA provides address translation mechanism under the control of the operating system which allows an application to access the HCA directly. 