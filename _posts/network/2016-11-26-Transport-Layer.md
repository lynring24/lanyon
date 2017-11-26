---
layout: post
title: Transport Layer
categories: Network
---
### Transport Services and protocols
- provides logical communication between application processes running on different hosts.
- transport protocols run in end systems.

### Sender / Receiver in transport layer
Sender : breaks application messages into segments, passes to network layer
Receiver : assembles the segmets into messages and passesto application Layer

>more than one transport protocol is available to applications (Internet uses TCP & UDP)

<table>
  <tr>
    <th> Transport </th>
    <th> Network  </th>
  </tr>
  <tr>
    <td>application vs application</td>
    <td> host vs host  </td>
    </tr>
</table>

### Multiplexing / Demultiplexing
Since there are lots of request and response comming in and out, multiplexer and demultiplexer are used to figure out where the packet is headed to. From sender, a packet departs through the multiplexer and "in-flight" on the link. Once the packet arrives at receiver side, by demultiplexer it is placed in a accurate port.

### Segments
what is needed:
- datagrams
- IP address of destination
- port # of destinaion
---
- IP address of source
- port # of source

Datagrams will be send to destination port number, but different source IP address is needed to distinguish with others. In UDP just after packet has arrived from upper layer, segments are passsed to network layer right away. This makes hard to find out the source whose sending the message. web servers have different sokets for each connecting clents. They create chile process to handle each connection. non-persistent HTTP will have different socket for each request.

TRANSPORT ---> TRANSPORT
NETWORK LAYER WITH SEGMENT
