---
layout : post
title : simple dijkstra
category : algorithm
description : dijkstra 알고리즘을 간단한 예제로 알아보기.
---

---

### Dijkstra 란?

**다익스트라 알고리즘**은 도로 교통망 같은 곳에서 나타날 수 있는 그래프에서 꼭짓점간의 최단 경로를 찾는 알고리즘이다.

---

### Dijkstra의 특징

변형이 많다.

원래 알고리즘은 두 꼭짓점 간의 가장 짧은 경로를 찾는 알고리즘이지만, 더 일반적인 변형은 한 꼭짓점을 "소스" 꼭짓점으로 고정하고 그래프의 다른 모든 꼭짓점까지의 최단경로를 찾는 알고리즘으로 최단경로트리를 만드는 것이다.
<center><img src = "https://upload.wikimedia.org/wikipedia/commons/2/23/Dijkstras_progress_animation.gif" width = "500"</center>>
(출처 - https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)

위 사진은 최단경로트리를 만드는 특징의 예시로 왼쪽 아래 시작점을 소스 꼭짓점으로 고정하고 가고자하는 꼭짓점까지의 최단경로트리를 만들고 있다.

---

### 알고리즘 설명

1. 배열을 통해서 모든 꼭짓점을 가지 않은 상태(미방문상태)로 표시한다.
2. 모든 꼭짓점에 시험적 거리값(무한대)을 부여한다. 시작하는 점은 초기점으로 거리는 0이 된다.
3. 현재 꼭짓점에서 미방문 인접 꼭짓점을 찾아 그 *시험적* 거리를 현재 꼭짓점에서 계산한다. 새로 계산한 *시험적* 거리를 현재 부여된 값과 비교해서 더 작은 값을 넣는다.

<img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EA%B0%B1%EC%8B%A0.png/220px-%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EA%B0%B1%EC%8B%A0.png">
(출처 - https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
현재위치에서 인접한 3개의 점까지 5의 거리로 도착할 수 있다고 하자. 주황색 점은 이미 다른 점에서부터 13의 거리로 도착할 수 있으므로(13<10+5) 갱신하지 않는다. 가운데 무한대 기호는 아직 방문하지 않았다는 기호이다. 따라서 현재위치거리 10에 5를 더한 15로 거리를 갱신한다. 오른쪽의 17은 다른 점에서 17의 거리로 왔는데 현재 위치에서 5만 이동하면 갈 수 있으므로(10+5<17) 15로 갱신한다.

4. 만약 현재 꼭짓점에 인접한 모든 미방문 꼭짓점까지의 거리를 계산했다면, 현재 꼭짓점을 방문한 것으로 표시하고 방문한 꼭짓점은 이후에는 다시 방문하지 않는다.

5. 두 꼭짓점 사이의 경로를 찾는 경우: 도착점이 방문한 상태로 표시되면 멈추고 알고리즘을 종료한다.

6. 완전 순회 경로를 찾는 경우: *미방문 집합*에 있는 꼭짓점들의 시험적 거리 중 최솟값이 무한대이면 이는 출발점과 미방문 집합 사이에 연결이 없는 경우이므로 멈추고 알고리즘을 종료한다.

7. 둘다 아니라면 시험적 거리가 가장 작은 다음 미방문 꼭짓점을 새로운 "현재 위치"로 선택하고 이어나간다.



---

### Pseudo code

```
function Dijkstra(Graph, source):
 2
 3      create vertex set Q
 4
 5      for each vertex v in Graph:    // 초기화
 6          dist[v] ← INFINITY         // 소스에서 v까지의 아직 모르는 길이
 7          prev[v] ← UNDEFINED        // 소스에서 최적 경로의 이전 꼭짓점
 8          add v to Q                 // 모든 노드는 초기에 Q에 속해있다 (미방문 집합)
 9
10      dist[source] ← 0               // 소스에서 소스까지의 길이
11
12      while Q is not empty:
13          u ← vertex in Q with min dist[u]    // 최소 거리를 갖는 꼭짓점
14                                              // 을 가장 먼저 선택한다
15          remove u from Q
16
17          for each neighbor v of u:           // v는 여전히 Q에 있다.
18              alt ← dist[u] + length(u, v)
19              if alt < dist[v]:               // v 까지의 더 짧은 경로를 찾았을 때
20                  dist[v] ← alt
21                  prev[v] ← u
22
23      return dist[], prev[]
```

---

<details>
<summary>참고문서</summary>
<div markdown="1">

- [DIJKSTRA - WIKIPEDIA](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
- [다익스트라의 개념](https://ratsgo.github.io/data%20structure&algorithm/2017/11/26/dijkstra/)


</div>
</details>
