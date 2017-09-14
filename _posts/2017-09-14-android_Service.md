---
layout: post
title: 서비스 Service
date: 2017-09-14 20:45:00
categories: Android
---
생각지도 않게 다른 어플을 띄우면 어플이 중단되는 문제점을 발견해서 백그라운드로 작업을 돌리기 위해 서비스를 사용했다.

## Service
주로 통신과 같은 무거운 작업들을 앞이 아니라 뒤에서 작업을 할 수 있도록 하는 앱구성 요소이다. 다운로드를 하거나 음악을 켜 놓은 상태에서 다른 작업을 하는 경우 등에 사용된다.<br>
서비스는 기본 thread에서 실행되기 때문에, CPU에 무거운 일을 처리할 때는 새 thread를 생성하여 처리하는게 좋다. 별도의 thread를 사용하면 '애플리케이션이 응답하지 않습니다(ANR)' 오류가 일어날 위험을 줄일 수 있다.<br>

## IntentService / BindService
 + IntentService<br>가장 간단한 형태의 서비스
 + BindService<br>activity와 상호작용할 수 있게 서비스를 묶는다

## [ITimeU/TimerService](https://github.com/lynring24/ITimeU)
IntentService가 아닌 BindService를 사용했던 이유는 UI작업을 위해 handler와 thread를 이용하기 위해서 였다. 물론, IntentService도 BroadcastReceiver를 사용해서 작업을 할 수 있지만, receiver에서 수행해야하는 다른 작업들도 많아서 BindService를 시도했다.
