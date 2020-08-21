---
layout: post
title: "K-means clustering 구현하기"
description: K-means clustering 구현하기
tags: Algorithm
---

- this post from [here](https://msc9533.github.io/2020/08/k-means-clustering/)

## K-means clustering

K-means clustering은 주어진 데이터를 k개의 클러스터로 묶는 알고리즘입니다.  
  
기본적인 동작원리는 데이터를 k개로 나누었을때 각 클러스터의 중심과의 거리차이의 분산을 최소화 하는 방식입니다. 
이 알고리즘은 Unsupervised Learning의 일종으로 label이 달려있지 않은 데이터에 label을 달 수 있습니다.

### Algorithm

K-means clustering은 다음과 같은 동작에 의해 수행됩니다.

1. k개의 데이터를 랜덤으로 중심점으로 설정.
2. 모든 데이터를 가장 가까운 중심점의 클러스터로 설정.
3. 각 클러스터 집단의 평균을 계산.
4. 평균값으로 중심점을 재설정.
5. 2번으로 돌아가 클러스터의 변화가 없을때까지 반복.

### 구현

```py
from math import sqrt
import matplotlib.pyplot as plt
import numpy as np
import random

"""
parameters
N : 각 ground truth 의 데이터 개수
k : 클러스터 개수, 총 데이터 개수는 N*k
sigma : random normal dataset의 sigma
centerRange : 중심점의 범위
"""
N = 200
k = 5
it = 0
sigma = 2.0
centerRange = (0,50)
# 중심점의 참값
GROUD_TRUTH = None
cluster = []
color_map = ["red", "orange", "yellow", "green", "blue"]
cluster_color = []

def getRandomDataSet(pointsNum,sigma = 1.0,centroids=4,center_range=(0,10)):
    """
    랜덤으로 생성된 중심점(centroids 개)으로부터 normal random으로
    각 pointsNum개의 데이터를 생성.
    """
    global GROUD_TRUTH,cluster,cluster_color
    gt_x = np.array(random.sample(range(center_range[0],center_range[1]),centroids))
    gt_y = np.array(random.sample(range(center_range[0],center_range[1]),centroids))
    # 중심점의 참값
    GROUD_TRUTH = np.stack((gt_x,gt_y),-1)
    result = np.zeros((pointsNum*centroids,2))
    cluster = [-1]*(pointsNum*centroids)
    cluster_color = ['black']*(pointsNum*centroids)
    for i in range(centroids):
        # normal random
        x = np.random.normal(loc=GROUD_TRUTH[i][0],scale=sigma,size=pointsNum)
        y = np.random.normal(loc=GROUD_TRUTH[i][1],scale=sigma,size=pointsNum)
        for j in range(pointsNum):
            result[i*pointsNum + j][0] = x[j]
            result[i*pointsNum + j][1] = y[j]
    return result

def plot(data,centroid):
    global it
    plt.clf()
    plt.scatter([p[0] for p in data],[p[1] for p in data],c=cluster_color)
    plt.scatter([p[0] for p in GROUD_TRUTH],[p[1] for p in GROUD_TRUTH],c='r',marker='s',s=100)
    if not centroid == None:
        plt.scatter([p[0] for p in centroid],[p[1] for p in centroid],c='m',marker='o',s=100)
        it+=1
        plt.title("iter = "+str(it))
    plt.grid(); plt.pause(0.1)

def getEuclideanDistance(p1,p2):
    return sqrt((p1[0]-p2[0])**2 + (p1[1]-p2[1])**2)

def getNearestNeighbor(points,p):
    # points 리스트로 부터 가장 가까운 점 반환
    minIndex = 0
    minValue = 9999
    for i in range(len(points)):
        tmpValue = getEuclideanDistance(points[i],p)
        if minValue > tmpValue:
            minValue = tmpValue
            minIndex = i
    return minIndex, points[minIndex]

def KMeansClustering(dataset,k=4):
    clusterChanged = True
    # k개의 데이터를 랜덤으로 중심점으로 설정
    sample_index = random.sample(range(0,len(dataset)),k)
    centroid = [dataset[i] for i in sample_index]
    # 클러스터의 변화가 없을때 까지 반복
    while clusterChanged:
        k_means = np.array([[0.0,0.0]]*k)
        k_nums = [0]*k
        clusterChanged = False
        for i in range(len(dataset)):
            # dataset을 가장가까운 중심점으로 클러스터 설정
            cluster_index , _ = getNearestNeighbor(centroid,dataset[i])
            k_nums[cluster_index] += 1
            # 각 클러스터의 평균 계산
            k_means[cluster_index] = (k_means[cluster_index]*(k_nums[cluster_index]-1) + dataset[i]) / k_nums[cluster_index]
            if cluster[i] != cluster_index:
                clusterChanged = True
                cluster[i] = cluster_index
                cluster_color[i] = color_map[cluster_index%5]
        # 계산된 평균으로 중심점 재설정
        centroid = [p for p in k_means]
        plot(dataset,centroid)


def main():
    dataset = getRandomDataSet(N,centroids=k,
                    center_range=centerRange,sigma=sigma)
    plot(dataset,centroid=None)
    KMeansClustering(dataset,k=k)
    plt.title('RESULT')
    plt.show()

if __name__ == "__main__":
    main()
    
```

### 구현 결과

![img](https://i.imgur.com/U3DimP8.gif)

### 한계점

![img](https://i.imgur.com/DIiorgk.png)  

클러스터의 개수가 실제보다 많거나 적은 경우 잘못된 지점을 중심점으로 선택하게 됩니다.  

![img](https://i.imgur.com/uk8cm5y.png)

초기 중심점을 선택할때 치우쳐 있는 중심점을 선택하면 가까운 분포를 포함하는 결과로 수렴합니다.(local minima)  

![img](https://i.imgur.com/MXMT4RW.png)

데이터의 분포가 구형분포가 아닌경우 잘못된 지점을 선택합니다.

---

<details>
<summary>참고문서</summary>
<div markdown="1">

- [k-means clustering - Wikipedia](https://en.wikipedia.org/wiki/K-means_clustering)
- <a href="https://medium.com/@rishit.dagli/build-k-means-from-scratch-in-python-e46bf68aa875#:~:text=K%2Dmeans%20clustering%20is%20a,without%20defined%20categories%20or%20groups).&text=The%20centroids%20of%20the%20K,assigned%20to%20a%20single%20cluster)">build-k-means-from-scratch-in-python</a>


</div>
</details>
