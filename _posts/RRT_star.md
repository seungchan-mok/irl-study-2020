---
layout: post
title:  Rapidly exploring Random Tree (RRT)
category: algorithm
description: RRT*
author: Inha Lee
---

## 개요
RRT와는 다르게 RRT_star는 트리를 구성하는 노드를 대체하여 비용을 줄일 수 있으면 기존 노드를 대체하여 트리를 구성합니다. 이 과정을 거치면 보다 최적의 경로가 나오게 됩니다.
## Algorithm

시작점으로부터 도착점까지 도달하는 RRT 알고리즘의 간단한 요약은 다음과 같습니다.

- parameter : 시작점( $Q_{init}$ ) 새로 생성된 노드( $Q_{new}$ ) 랜덤 노드( $Q_{rand}$ )
- while(도착점에 도착할 때까지)
  - [1] 랜덤 노드를(임의의 점)지정한다.
  - [2] 랜덤 노드로부터 가장 가까운 노드를(트리에 달려있는) 선택한다.
  - [3] 랜덤 노드-가장 가까운 노드간 방향과 step을 고려하여 새로운 노드를 선정한다.
  - [4] 만약 장애물하고 충돌이 나지 않으면.
    - (a) 새로운 노드로부터 가까운 노드들을 선택합니다. 
    - (b) 가장 가까운 노드 중 제일 낮은 cost를 가진 노드와 새로운 노드를 연결합니다.
    - (c) cost를 참고하여 가장 가까운 노드들의 트리중 더 좋은 방법이 있는지 찾습니다. 이 과정은 [Dijkstra](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98) 알고리즘과 유사합니다.
    - (d) 트리를 재구성합니다.

![](https://d3i71xaburhd42.cloudfront.net/60324fd5346b86a4821c8e36137b7bfb860a0165/4-Figure1-1.png)
[출처](https://www.semanticscholar.org/paper/Arm-Trajectory-Generation-Based-on-RRT*-for-Robot-Lee-Baek/60324fd5346b86a4821c8e36137b7bfb860a0165)




![](https://t1.daumcdn.net/cfile/tistory/2415D33D54EA8AB61A?download)
### 결과

![](https://imgur.com/9aCP9fo.png)

위 예제를 실행하면 그림과 같은 결과를 얻을 수 있습니다.

---


<details>
<summary>참고문서</summary>
<div markdown="1">

- [Improving the Optimality of RRT: RRT*](http://joonlecture.blogspot.com/2011/02/improving-optimality-of-rrt-rrt.html)
- [Optimal Path Planning using RRT_star based
Approaches A Survey and Future Directions](https://www.researchgate.net/publication/311394143_Optimal_Path_Planning_using_RRT_based_Approaches_A_Survey_and_Future_Directions)
- [Informed RRT*: Optimal Incremental Path Planning Focused through an Admissible Ellipsoidal Heuristic](https://www.researchgate.net/publication/261512737_Informed_RRT_Optimal_Incremental_Path_Planning_Focused_through_an_Admissible_Ellipsoidal_Heuristic)

</div>
</details>