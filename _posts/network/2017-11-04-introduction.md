---
layout: post
title: Introduction of Network
categories: Network
---

 Internet, that is what we are surrounded by.
 We learn that it is network of networks, an infrastructure for providing network applications and it provides program interface for application.
 Last semester I've taken a web system programming class, programming a web application and learn about http and jsp as a preview of network.

# Internet, Web and Protocol
#### Internet
- network of networks
- infrastructure for providing network applications
- provides program interface for application

#### Web(World Wide Web)
- just one of the way to send information in internet (another example might be a Mail Service (port : 25))
- uses http for Protocol
- hyper text and URLs

#### Protocol
- an agreement of message format, order and actions to operate when messsage is transmitted/received for communication between hosts.

# Internet Elements
  - host/terminal/end system
  - access network
  - physical media
  - network core

### 1. access network
- Residential(home) access network
- Enterprise access network
-  Mobile access network.

<pre>
  a. Residential(home) access network
  Techniques used at home access network are ADSL(asymmetric digital subscriber line) and Cable. ADSL modem at home is conneted to the centeral office, which has dsl multiplexer. Then, the central office connects the line to ISP. <br>On the other hand, cables are connected to headend(Cable Modem Termination System). CMTS connects the line to ISP.

  b. Enterprise access network( Ethernet )

  c. Mobile access network <br>
  Techniques used for mobile access nets are divided by the range it could cover. Wireless LAN is for local. WAN is for wide area, works in cellular units. There are also PAN and etc.
</pre>

### 2. Phsical Media
- Guided Medias : Copper, Coaxial, fiber Optic Cable<br>
- Unguided Medias : radio, satellites

### 3. Network Core
- Global ISPS
- Regional ISP and CDN (Content Distributon Network)

Global ISPs have much bigger range than Regionl ISPS.
CDN is served at core ~ access networks but depends on where and how it is served. It could be 'enter deep' near the accenss network or could be 'bring home' at upper layer than access network.</pre>

# How does the hosts exchange messages?
  There used to be 3 ways ; circuit switching, message swiching, packet swtiching but, message swiching has been depreciated.
- circuit switching

Resouces used for exchanging messages such as physical links are dedicated and determined before the actual transmission.
There must be a setup before always.
Therefore, messages are guaranteed.
Usually used for telephone wires.

- packet switching

Messages are torn down into 'packets' and sent by one hop between routers.
Since this method is based by 'store and forward', the packets could not move until the full parcket arrived at the destination router.
Unlike circuit swiching, this could handle more users(cliets) with composure.<br> However if the rate of arriving packet exceed the butffer of router or the rare of transmission of router, the packet will be dropped or lost.
