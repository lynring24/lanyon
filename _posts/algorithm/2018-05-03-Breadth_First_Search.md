---
layout: post
title: Breadth First Search(BFS)
categories: Algorithm
---
탐색 트리의 수평 방향으로 루트 노드부터 목표노드까지 탐색을 진행 <br>
자료구조 : Queue
<table>
<tr>
<td>장점</td><td>단점</td>
</tr>
<tr>
<td>최단 경로 보장<br> 노드가 적고, 깊이가 얕은 트리에서 유리 </td>
<td> 열린 노드들을 관리하므로 공간 복잡도가 크다. </td>
</tr>
</table>

평균 탐색 노드 수 (가지 b개, 목표 노드 : d) = d-1까지의 탐색 + d층에서 중간
d-1까지:  1 + b + b^2 + b^3 + .. + b^(d-1) = b^d-1 / b-1<br>
d 중간 : ( 1/2 )* b^d
