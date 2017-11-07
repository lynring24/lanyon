---
layout: post
title: Application Layer
date: 2017-11-08 01:10:00
categories: Network
---

 Applications are what people use. It could be a mail service, Internet and etc. <br>
 Application layer protocols support these network application, sending message in right format, order and other operation needed to handle messages.

### Architecture
 A. Client and Server <br>
  <pre>
  Server waits for client to call and ask for the service and client starts the connection(exchane message).
  Since server has to handle multiple calls from N-clients, it doesn't have a scalability.
  </pre>    
 B. Peer to peer (P2P)
 <pre>
  The end system itself is a client and a server. Hosts are logically connected.
  New peer becomes new server so p2p architectures have scalability.
</pre>
### Process and Socket
<pre>
Process is an operation(or could be a program) run on host.

if client == server (on same host)  process is inter-leaved or else the message from process will be send by socket.

Socket controls how process being sent with parameters, located in higher level than transport level.
Once the message passes through the socket, remain works are up to OS.
</pre>
### Protocol and Transport service
####  Protocol of this level hanles
  1. message type = (request or response)
  2. check the syntax of message
  3. semantics of message
  4. when and how to send/receive

#### Transport service should consider
  1. reliability = duplicaiont x / error x / right order
  2. delay(timing)
  3. throughput = required minimum bandwidth
  4. security

>  Since TCP doesn't support security, SSL(Secure  Socket Layer) is used. SSL is a Socket API above transport layer.

### TCP / UDP
<table style="width:100%">
  <tr>
    <th></th>
    <th>TCP</th>
    <th>UDP</th>
  </tr>
  <tr>
    <td>reliability</td>
    <td>O</td>
    <td>X</td>
  </tr>
  <tr>
    <td>flow control</td>
    <td>O</td>
    <td>X</td>
  </tr>
  <tr>
    <td>congestion control</td>
    <td>O</td>
    <td>X</td>
  </tr>
  <tr>
    <td>connection-oriented</td>
    <td>O</td>
    <td>X</td>
  </tr>
  <tr>
    <td>timing</td>
    <td>X</td>
    <td>X</td>
  </tr>
  <tr>
    <td>throughput</td>
    <td>X</td>
    <td>X</td>
  </tr>
  <tr>
    <td>security</td>
    <td>X</td>
    <td>X</td>
  </tr>
</table>
