---
layout: post
title:  PRM with MAT(Medial Axis Transformation) 
category: algorithm
description: Medial Axis를 이용해서 Path Planning을 해보자
---
# PRM with MAT(Medial Axis Transformation) 
#### Skeletonization 을 활용한 Path Planning
---

### Medial Axis?
--- 
2차원 또는 3차원 형상의 뼈대, 
![](https://imgur.com/NhIJGdF.png)

### 거리변환행렬
임의의 1인 point로부터 0인 포인트 까지의 거리(거리를 밝기로 표현)
![](https://mblogthumb-phinf.pstatic.net/20140110_149/pckbj123_1389333471404nLXtG_JPEG/3.jpg?type=w2)![](https://mblogthumb-phinf.pstatic.net/20140110_274/pckbj123_1389333471537zeo48_JPEG/6.jpg?type=w2)
- 출처:[OpenCV 손 동작 인식, 거리 변환 행렬(Distance Transform)을 이용한 손바닥 중심 구하기](https://m.blog.naver.com/PostView.nhn?blogId=pckbj123&logNo=100203325426&proxyReferer=https:%2F%2Fwww.google.com%2F) 

### 보르노이 다이어그램
점들을 영역으로 분할한 다이어그램

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/Euclidean_Voronoi_diagram.svg/1024px-Euclidean_Voronoi_diagram.svg.png)
출처: [위키피디아: 보로노이 다이어그램](https://ko.wikipedia.org/wiki/%EB%B3%B4%EB%A1%9C%EB%85%B8%EC%9D%B4_%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8)
### MAPRM (Medial Axis Probailistic RoadMap)
로봇의 경로생성에 쓰인다 벽이나 장애물로부터 가장 먼 지점을 path로 지정하기 때문에 안전한 경로를 생성할 수 있다.
![](https://imgur.com/wnXU5Wv.png)
---
MAPRM Algorithm
1. N번 반복
   1. 무작위 점 p를 잡는다
   2. if(p가 C_free 안에 있다면)
      1. 벽이나 장애물 중 가장 가까운 점 q 를 찾는다
      2. p인 점으로부터 qp방향으로 q 와 크기가 같아지는 q`가 있을 때까지 움직임
   3. else
      1. 벽이나 장애물 중 가장 가까운 점 q 를 찾는다
      2. q인 점으로부터 qp방향으로 q 와 크기가 같아지는 q`가 있을 때까지 움직임
   4. 확정지은 위치가 path

---
## 참고 문헌
[1] [Jyh-Ming Lien, S. L. Thomas and N. M. Amato, "A general framework for sampling on the medial axis of the free space," 2003 IEEE International Conference on Robotics and Automation (Cat. No.03CH37422), Taipei, Taiwan, 2003, pp. 4439-4444 vol.3, doi: 10.1109/ROBOT.2003.1242288](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=1242288)

[2] [Jory Denny, Evan Greco, Shawna Thomas, and Nancy M. Amato, MARRT: Medial Axis Biased Rapidly-Exploring Random Trees](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.432.7837&rep=rep1&type=pdf)