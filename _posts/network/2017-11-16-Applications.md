---
layout: post
title: Applications
categories: Network
---
# Applications
  - Web
  - Mail
  - Domain Name system
  - Multimedia with Content Distribution Network

##  World Wide Web
Web is a service between browser(client) and web server. <br>
Browser request HTML file with objects and server response by sending it.

#### Protocol : HTTP
HTTP works above TCP. Since TCP is connection-oriented, http needs setup( 3 way handshacking ).
  1.  client requsets server
  2.  server accepts or refuses.
  3.  if accepted, client request for base HTML file
  4.  server passes the file to client

HTTP could be divided into persistent HTTP and non-persistent HTTP
  - non-persistentt HTTP : end the connection just after one object is arrived
  - persistent HTTP : keeps the connection until every objects had arrived or the time out
  - non-persistent HTTP could work in parallel thread but still there could be delay for buffer

HTTP is statelss which means it doesn't care or store backlogs. To support the state, cookie file is used instead.

##### Web Cache
Browser could request a file through web cache if there are file it wants rather than accessing the original server. Requesting delay became shorter and the traffic for link and original server has een distributed. However, the files in cache could be out-dated ones so web cache asks the original server if there are any changes before response. This is called a 'conditional get'.

## Mail
Mail systems contain three components : User Agent, Mail server , SMTP protocol.<br>
Client writes mail through user agent. Then the agent send the mail to writer's mail server by SMTP and put in the mail buffer. Mail server opens the TCP and passes the mail to receiver's mail server and put it in receiver's mail box. On receiver side, receiver opens mail by using POP3 or IMAP.

#### Access Protocol
 - SMTP
 - IMAP
 - POP3
 - HTTP

## Domain Name system
What humans are familiar to is the domain name.
