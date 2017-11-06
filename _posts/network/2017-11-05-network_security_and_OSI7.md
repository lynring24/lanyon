---
layout: post
title: Introduction of Network
categories: Network
---
Networks are constructed in layers. It's because by modulization, the operation or roles of each layer could be specified and easy to maintain. On the other hand, the work of security should be done on every layers.

# Network Stack (OSI/Internet)
 According to ISO/OSI layers, it's divided into 7 parts, but Internet consider it to be 5.
<br>
<pre>
  7 Application    Supports network application
  6 Presentation   Data Interpretation such as encryption
  5 Sessoin       checkpointing, syncrnizin, recover from crashes
  4 Transport     process - procses data transfer Protocol
  ---
  3 Network       routes the datagram, routing is done here
  2 Link          node to node data transfer
  1 Physical      bits on wires
  </pre>
<br>
Only the end system handles from transort level to application (all the 7layers). Router handles from Network to physical and switches  works from links to physical layer.

## Encapsulation / Decapsulation
<pre>
application     message
transport       message segment
network         message segment datagram
links           message segment datagram frame  </pre>
  <br>
  Encapsulation : message  from higher level is wrapped with the data(lower level protocol) as a header.<br>
  Decapsulation : opposite of encapsulation, router unwrapps the header to check out the destination of packet.

# security

On client Side
  - worm
  - virus
  - spyware
  - botnet
On Server
  - DoS, DDos
On link
  - Packet Sniffing
  - IP Spoofing
