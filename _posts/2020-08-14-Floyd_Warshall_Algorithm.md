---

layout : post

title : Floyd-Warshall Algorithm

category : algorithm

description : Floyd-Warshall Algorithm을 간단히 알아보자.

---

그래프에서 정점끼리의 최단 경로를 구하는 방법

1. 하나의 정점에서 다른 하나의 정점까지의 최단경로
2. 하나의 정점에서 다른 모든 정점까지의 최단경로
3. 하나의 목적지로 가는 모든 최단 경로
4. 모든 최단 경로

Floyd-Warshall Algorithm은 (4).모든 최단 경로를 구할 때 사용하는 알고리즘이다. 





# Floyd-Warshall Algorithm이란?

변의 가중치가 음이거나 양인 (음수 사이클은 없는) 가중그래프에서 최단경로를 찾는 알고리즘이다.

***

## Dijkstra Algorithm과 다른점

1. 모든 노드 쌍에 대해 최단거리를 구한다.
2. 노드에서 음의 가중치를 가지고 있을 때도 사용 가능하다.
3. 다익스트라 알고리즘은 시간 복잡도가 O(v^2)이고 플로이드 워셜 알고리즘은 O(v^3)이다.
4. 중간경로에 들어갈 수 없는 경우 아예 계산을 안하기 때문에 다익스트라 알고리즘보다 빠르다.

***

### Example


![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/floyd_warshall_1.PNG?raw=true)

![2](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/floyd_warshall_2.PNG?raw=true)

![3](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/floyd_warshall_3.PNG?raw=true)

![4](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/floyd_warshall_4.PNG?raw=true)



```
---

<details>
<summary>참고문서</summary>
<div markdown="1">

- [플로이드-워셜 알고리즘](https://namu.wiki/w/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%85%9C%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
- [플로이드-워셜 알고리즘](https://m.blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221234427842&proxyReferer=https:%2F%2Fwww.google.com%2F)

</div>
</details>
```