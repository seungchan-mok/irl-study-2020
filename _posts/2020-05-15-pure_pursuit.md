---
layout: post
title:  pure_pursuit이란?
category: algorithm
description: pure_pursuit 알고리즘을 간단한 예제로 알아봅니다.
---

## Pure pursuit 개요
pure pursuit은 차량이 현재위치에서 목표점까지 이동하기 위한 곡률을 계산해 작동하는 경로추종 알고리즘입니다. 이 알고리즘의 포인트는 차량에서 일정거리 앞에 위치한 경로상의 목표점을 선택하는 것입니다. 

---

## Pure pursuit 이론

Pure pursuit의 기하학적 모델링과 중요 파라미터인 Look-ahead-distance에 대해 알아보겠습니다.

### 1. Geometry of pure pursuit model 
<center><img src = "https://media.springernature.com/lw785/springer-static/image/chp%3A10.1007%2F978-3-319-62434-1_40/MediaObjects/454216_1_En_40_Fig2_HTML.gif" width = "500"></center>

    차량조향각에 대한 모델링은 위 그림과 같습니다. 위 모델링을 통해 Pure pursuit 알고리즘에서 사용되는 목표지점(Gx,Gy)를 추종하기 위한 차량의 조향각(세타)을 구할 수 있습니다.
    
    수학적으로 계산한 차량조향각 세타는 아래와 같습니다.

<center><img src ="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRfKpsXg_EoaINoz5270eLjItTsPO3gSOF_OIMPgagTjxtr-tpE&usqp=CAU"></center>

### 2. Look-ahead-Distance(LD)

    Pure pursuit 알고리즘에서 Look-ahead-distance는 차량의 후륜에서 목표지점까지의 직선거리를 의미합니다. Look-ahead-distance를 어떻게 설정하느냐에 따라 경로추종방식이 변화하기 때문에 Look-ahead-distance를 어떻게 설정하느냐는 매우 중요합니다.

    1) LD를 짧게 설정할 경우 : 차량이 경로상으로 빠르게 복귀해야하는 경우에는 Look-ahead-distance를 짧게 설정해야합니다. 하지만, 너무 짧게 설정할 경우 횡방향 오실레이션이 발생할 위험이 있습니다.

    2) LD를 길게 설정할 경우 : 차량이 경로를 부드럽게 주행하기 위해서는 Look-ahead-distance를 길게 설정합니다. 하지만, 너무 길게 설정할 경우 코너 근처에서 더 큰 곡율이 발생할 수 있고, 경로추종의 성능이 저하될 수 있습니다.




---  

## Pure pursuit Argorithm
1. 차량의 현재 위치를 결정한다.
2. 차량에서 가장 가까운 경로상의 점을 찾는다.
3. 목표점을 찾는다.   
4. 곡률을 계산하고 해당 곡률로 차량의 heading을 업데이트해준다.
5. 차량의 위치를 업데이트한다.


  
<br/>
<br/>



### 1)  차량의 현재 위치를 결정한다.  
* global좌표에서의 현재 차량의 위치 (x,y,th)를 받아서 저장합니다.  
<br/>
<br/>


### 2) 차량에서 가장 가까운 경로상의 점을 찾는다.
* path의 모든점들을 순환하면서 현재위치에서 가장 가까운점을 찾습니다. 이때, 차량이 뒤로 가는 것을 방지하기 위해서 만약, 이전에 찾은 path상의 점이 있다면 가장 가까운 점을 찾기위한 시작 인덱스를 그 점으로부터 시작합니다.
<br/>
<br/>


### 3) 목표점을 찾는다.
* 차량의 위치에서 LD반경 안에 path와의 교차점이 있다면 그것을 목표점으로 삼습니다. 
<br/>
<br/>


### 4) 곡률을 계산하고 해당 곡률로 차량의 heading을 업데이트 해준다. 
* 차량의 곡률은 위에서 설명했던 것과 같이 현재 차량의 위치, 목표점을 이용해 구합니다. 이때, 차량heading의 방향을 정확하게 알기 위해서 차량의 벡터와 LD의 벡터를 Cross product연산을 통해 plus이면 오른쪽방향 negative이면 왼쪽방향으로 heading을 결정하고, 구해진 곡률로 차량의 heading을 업데이트 해줍니다.
<br/>
<br/>


### 5) 차량의 위치를 업데이트한다.
* global좌표에서의 현재 차량의 위치 (x,y,th)를 받아서 저장합니다.




----
