---
layout: post
title: "SVD(Singular Value Decomposition)"
description: SVD의 이해, 활용
tags: 선형대수
---

# SVD(Singular Value Decomposition)

## 먼저 알아두어야 할 내용
- 기저 행렬

---
  x, y ,z 축에 대한 단위벡터 행렬
  
  $$
  i = (1,0,0),\quad
  j = (0,1,0),\quad
  k = (0,0,1)
  $$

- 벡터의 선형 변환

---

$$
T(c(\vec{a}+\vec{b})) = cT(\vec{a})+cT(\vec{b})
$$

위와 같은 성질에 따라 기존의 좌표는 다음과 같이 나타낼 수 있다

$$
T\left(
\begin{bmatrix}
a\\
b 
\end{bmatrix}`
\right)
=
aT\left(
\begin{bmatrix}
1\\
0 
\end{bmatrix}
\right)
+
bT\left(
\begin{bmatrix}
0\\
1 
\end{bmatrix}
\right)
$$

즉, 새로운 백터 기저

$$
T\left(
\begin{bmatrix}
1\\
0 
\end{bmatrix}
\right)
,\quad
T\left(
\begin{bmatrix}
0\\
1 
\end{bmatrix}
\right)
$$

의 a배와 b배의 합으로 나타내진다.

다시 말해 새로운 기저에서의 $\vec{a}$+$\vec{b}$ 이다.

$$
x=
\begin{bmatrix}
1\\
1 
\end{bmatrix}\quad
A=
\begin{pmatrix}
2 & -3\\
1 & 1
\end{pmatrix} \\
A \vec{x} = ?
$$  
  
- [선형변환 해보기-공돌이의 수학정리노트](https://angeloyeo.github.io/p5/Matrix_as_a_linear_transformation/transformation1/)  

- 내적은 행렬의 곱으로 나타낼 수 있다.  


u = <$u_a,u_b,u_c$>  v = <$v_a,v_b,v_c$>


$$
u \cdot v = u_a v_a+u_v b_b+u_c v_c\\
=\begin{pmatrix}
u_a & u_b & u_c
\end{pmatrix}

\begin{pmatrix}
v_a \\
v_b \\
v_c
\end{pmatrix} 
= uv^T
$$


- 직교행렬 (Orthogonal Matrix)   

다음과 같은 식을 만족하는 행렬을 직교행렬이라고 한다.
$$
U^TU = I
$$

$$
I=\begin{pmatrix}
1   & 0   & 0   & ... & 0\\
0   & 1   & 0   & ... & 0\\
0   & 0   & 1   & ... & 0\\
... & ... & ... & ... & 0\\
0   & 0   & 0   & 0   & 1 
\end{pmatrix}
$$

직교행렬의 성질을 알아보기 위해 다음과 임의의 직교행렬 W에 대해 같이 전개를 해보겠다

$$
a = (a_1,a_2,a_3), \quad
W=\begin{pmatrix}
- & a & - \\
- & b & - \\
- & c & - \\
\end{pmatrix}
$$

전치행렬은

$$
W^T = \begin{pmatrix}
| & | & | \\
a^t & b^t & c^t \\
| & | & | \\
\end{pmatrix}\\
$$

이 둘을 곱하면

$$
WW^T = \begin{pmatrix}
aa^t & ab^t & ac^t \\
ba^t & bb^t & bc^t \\
ca^t & cb^t & cc^t \\
\end{pmatrix}
\\ \quad\\\quad\quad\quad
= \begin{pmatrix}
a\cdot a & a\cdot b & a\cdot c \\
b\cdot a & b\cdot b & b\cdot c \\
c\cdot a & c\cdot b & c\cdot c \\
\end{pmatrix}
\\ \quad\\\quad\quad\quad
= \begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{pmatrix}
$$


즉, 직교행렬이란 행렬안의 모든 행, 열 벡터들이 자기 자신을 제외한 모든 행,열 벡터들과 직교인 동시에 단위 벡터인 행렬을 말한다.

또한 다음과 같은 성질을 가진다.

$$
U^TU = I,\quad U^{-1}U=I \quad => \quad U^T= U^{-1}
$$


- 대각행렬 (Diagonal Matrix)

---

대각성분을 제외한 나머지 원소의 값이 0인 행렬을 말한다

$$
\Sigma=\begin{pmatrix} \\
 \sigma_1  & 0   & 0   & ... & 0 \\
0   &  \sigma_2   & 0   & ... & 0 \\
0   & 0   &  \sigma_3   & ... & 0 \\
... & ... & ... & ... & 0 \\
0   & 0   & 0   & 0   &  \sigma_n \\
\end{pmatrix}
$$

만약 $\Sigma$ 가 M X N 일 때 M > N 이라면 

$$
\Sigma=\begin{pmatrix}
 \sigma_1  & 0   & 0   & ... & 0\\
0   &  \sigma_2   & 0   & ... & 0\\
0   & 0   &  \sigma_3   & ... & 0\\
... & ... & ... & ... & 0\\
0   & 0   & 0   & 0   &  \sigma_n\\
0   & 0   & 0   & 0   & 0\\
... & ... & ... & ... & ...\\
0   & 0   & 0   & 0   & 0\\
\end{pmatrix}
$$

---

# SVD

임의의 행렬 A에 대하여 다음과 같이 행렬을 분해할 수 있다.

$$
A=U\Sigma V^T\\
$$

A : m $\times$ n 인 임의의 행렬(선형변환에 사용하는 행렬)

U : m $\times$ m 인 직교행렬(선형변환 후 행렬)

$\Sigma$ : m $\times$ n 인 대각행렬(선형변환 후 크기)

V : m $\times$ n 인 직교행렬(선형변환 전 행렬)



설명을 위해 선형 변환의 예제를 보겠다.

벡터 $\vec{x}$를 다음과 같은 행렬 A를 이용하여 선형변환하면($A\vec{x}$를 구하면)

$$
A = \begin{pmatrix} 
0.25 & 0.75 \\
1 & 0.5 \\
\end{pmatrix}
$$


![](https://imgur.com/YnNWkPm.gif)  

위 그림을 보면 선형변환을 하면 크기 또한 변한다는 것을 알 수 있다. 

이번에는 직교하는 두 벡터를 선형변환하면

![](https://imgur.com/utoL1hL.png)

[직교벡터 선형변환 보조자료 - 공돌이의 수학정리노트](https://angeloyeo.github.io/p5/2019-08-01-preview_SVD/)

위 그림과 같은 변환이 나온다.

$$
A=U\Sigma V^T\\
$$

라는 식은 다음과 같은 선형변환 수식으로부터 유도되었다

A : m $\times$ n 인 임의의 행렬(선형변환에 사용하는 행렬)

U : m $\times$ m 인 직교행렬(선형변환 후 행렬)

$\Sigma$ : m $\times$ n 인 대각행렬(선형변환 후 크기,특이값)

V : m $\times$ n 인 직교행렬(선형변환 전 행렬)


직교행렬 V를 임의의 행렬 A를 이용하여 선형변환을 하면

$$
AV=X(변환된 행렬)
$$

[만약 선형 변환을 한 뒤에도 두 벡터가 직교를 한다면](https://angeloyeo.github.io/p5/2019-08-01-preview_SVD/) 이를 다시 단위행렬과 그 크기로 나타낼 수 있다.

$$
AV=\Sigma U
$$

이 때 다음과 같은 직교행렬 성질 때문에

$$
V^T = V^{-1}
$$

식을 다시

$$
A=U\Sigma V^T\\
$$

과 같이 나타낼 수 있다.

이 식은 다음과 같은 시각으로도 볼 수 있다.

## 임의 행렬 A를 정보량에 따라 쪼갤 수 있다.

$$
A=U\Sigma V^T\\
$$

는

$$
 = \begin{pmatrix}
| & | & ... & | \\
\vec{u_1} & \vec{u_2} & ... &\vec{u_m} \\
| & | & ... &| \\
\end{pmatrix}
\begin{pmatrix}
 \sigma_1  & 0   & 0   & ... & 0\\
0   &  \sigma_2   & 0   & ... & 0\\
0   & 0   &  \sigma_3   & ... & 0\\
... & ... & ... & ... & 0\\
0   & 0   & 0   & \sigma_m & 0
\end{pmatrix}
\begin{pmatrix}
- & \vec{v_1}^T & - \\
- & \vec{v_2}^T & - \\
- & ... & - \\

- & ... & - \\
- & \vec{v_m}^T & - \\
\end{pmatrix}\\
$$
  
$$
= \sigma_1\vec{u_1}\vec{v_1}^T + \sigma_1\vec{u_1}\vec{v_1}^T +... +\sigma_m\vec{u_m}\vec{v_m}^T
$$
와 같이 나타낼 수 있는데 이는 A행렬을 동일한 m $\times$ n 크기를 갖는 행렬들의 합으로 나타낼 수 있다는 것이다.

- full SVD
  
![](https://imgur.com/8ZzeePo.png)


- thin SVD
  (행렬 크기를 맞춰주기 위해 넣었던 0을 모두 지움)  

![](https://imgur.com/asyUqMy.png)

- Compact SVD(크기가 0인 특이값들을 날림)  
  
![](https://imgur.com/BYHrq5N.png)

- [Truncated SVD](https://angeloyeo.github.io/p5/2019-08-01-SVD_picture_applet/)
  (크기가 큰 t개의 특이값들만을 남김)  
![](https://imgur.com/154sAWH.png)

## pseudo inverse를 할 수 있다.
구할 수 없던 역행렬을 구할 수 있게 해준다.

그 전에 몇가지 정의가 필요하다.

- 역행렬을 구할 수 없는 행렬 A의 역행렬을 $A^+$와 같이 표현한다.
- $\Sigma$의 역행렬 $\Sigma^+$를 다음과 같이 정의한다.
 
$$
\Sigma=\begin{pmatrix}
1\over\sigma_1  & 0   & 0   & ... & 0\\
0   &  1\over\sigma_2  & 0   & ... & 0\\
0   & 0   &  1\over\sigma_3   & ... & 0\\
... & ... & ... & ... & 0\\
0   & 0   & 0   & 0   &  1\over\sigma_n 
\end{pmatrix}
$$

SVD의 기본 식은

$$
A=U\Sigma V^T\\
$$

이고 다음과 같이 나타낼 수 있다

$$
A^+=U^T\Sigma^+ V\\
$$

즉 A의 역행렬 $A^+$를 손쉽게 구할 수 있다.

ex)

$$
Ax = B\\
A^+Ax =A^+B\\
x=  A^+B 
$$