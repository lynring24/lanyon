---
layout: post
title: Depth First Search(DFS)
categories: algorithm
tags: [algorithm, search]
---
탐색 트리의 수직 방향으로 점차 깊은 곳까지 목표노드를 찾아 탐색해 나가는 기법 (BackTracking 존재) <br>
자료구조 : Stack
<table>
<tr>
<td>장점</td><td>단점</td>
</tr>
<tr>
<td>저장공간의 수요가 비교적 적다. <br>목표노드가 깊은 단계에 있는 경우 해를 구하기 쉽다. </td>
<td>해가 없는 경우, 깊이 빠진다. <br>최단 경로를 보장하지 않는다. </td>
</tr>
</table>

평균 탐색 노드 수 (가지 b개, 목표 노드 : d) = (최좌즉 + 최우측) /2<br>
 최좌측 = d+1 <br>
 최우측 = 1 + b + b^2 + b^3 + .. + b^d = b^(d+1)-1 / b-1<br>
