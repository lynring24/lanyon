---
layout: post
title: network setting in Ubuntu 16.04/ 18.04
categories: Network
---

연구실 서버를 이전하게 되면서 서버 셋팅이 꼬였다. 간단하게 필요한 command를 정리해봤다. 특히 Mellanox ConnectX-3은 선의 상태, 서버의 셋팅 
그리고 스위치의 상태가 모두 잘 맞기가 어려워 고생을 했었다. 

# get IP setting 
## ubuntu 16.04 
```
$vi  /etc/network/interfaces
$ service networking restart
```
## ununtu 18.04
```
$ vi /etc/netplan/*.yaml
$ netplan apply 
```
# get network card info with vendor, logical name, capacity 
```
$ lshw -C network  | grep -e 'vendor\|logical name\|capacity'
```
# get speed of nic cart
```
$ ethtool LOGICAL_NAME | grep Speed
```
