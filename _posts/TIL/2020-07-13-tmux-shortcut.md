---
layout: post
title: tmux shortcut
categories: TIL
---

```
# PREFIX  = <CTRL-B>

# pane
$ PREFIX %   # 세로로 pane 가르기 
$ PREFIX "   # 가로로 가르기 

# window
$ PREFIX c   # 탭 열기 
$ PREFIX N   # 해당 탭 번호로 이동하기 
$ PREFIX &   # 탭 종료
$ PREFIX p   # 이전 탭으로 이동 
$ PREFIX n   # 다음 탭으로 이동

# session 
$ tmux ls
$ tmux attach  # 세션을 불러온다. 
$ PREFIX d   # 해당 탭에서 나가되, 프로세스는 유지 
$ tmux kill-session –t N     # 세션을 죽인다.  
$ tmux has-session –t TARGET_SESSION  # TARGET_SESSION이라는 이름의 세션이 열려있는지 확인
$ tmux attach-session –t TARGET_SESSION  # TARGET_SESSION이라는 이름의 세션을 가져온다. 
```
