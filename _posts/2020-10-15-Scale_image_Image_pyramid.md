---

layout : post

title : Scale Space & Image pyramid

category : basic of image processing

description : 이미지의 스케일을 다루는 방법을 알아보자.
---

원래는 sift에 대해 써보려고 했으나 기초가 되는 지식들이 너무 부족하여 밑에서부터 알아보자는 생각으로 이번 post를 작성하였습니다.



이미지에서  scale을  다루는 방법

1. Scale Space
2. Image Pyramid



# Scale이란 무엇인가?

풍경을 멀리서 보거나, 일부분을 확대해서 보거나 하는 척도이다.

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/city1.jpg?raw=true)



​                                                                ![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/zoom.JPG?raw=true)\

Scale을 표현할 때 첫 번째 사진처럼 멀리서 보아서 풍경이 다 보이는 것을 Scale이 크다고 하고

두 번째 사진처럼 어느 부분을 확대해서 보는 것을 Scale이 작다고 한다.

## Scale이 중요한 이유

어떤 이미지를 볼 때 전체적으로 확인해야 하는 경우와 일부분을 자세히 확인해야 하는 경우들이 생기기 때문이다.

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/scale_curve.png?raw=true)

위 사진을 큰 스케일로 보게 되면 곡선이 있고 curve가 있는 것을 알 수 있다. 하지만 작은 스케일로 보게 된다면 직선이라고 생각할 수 밖에 없다.

이러한 문제를 해결하기 위한 방법으로 Scale space와 Image pyramid 방법이 있다.



**Image pyramid**

----

정의 : 이미지의 크기를 줄여가면서 분석하는 작업을 통해 생성된 이미지의 집합

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/Image_pyramid.png?raw=true)

이미지의 원본을 Level 0으로 하고 작은 사진으로 갈 수록 Level 뒤의 숫자를 1씩 증가하면서 읽어준다.

---

피라미드의 종류

1. 가우스 피라미드

    후속 이미지는 가우시안 평균을 사용하여 가중치를 부여 하고 축소한다. 보통 텍스처 합성에 많이 사용 된다. 가우스 피라미드에서 블러링에는 가우시안 필터를 적용하고, 다운샘플링은 짝수번째 픽셀들은 버리고 홀수번째 픽셀들을 선택하는 방법을 쓴다.

   ![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/Gausian_pyramid_ex.jpg?raw=true)

   

   

2.  라플라시안 피라미드

   가우시안 피라미드와 매우 비슷하지만 레벨이 높아질수록 이미지의 흐릿함을 증가시키며 저장한다. 고해상도 이미지를 재구성 할 수 있고, 이미지 압축 기술에 많이 사용 된다

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/Laplacian_pyramid_ex.jpg?raw=true)

### Scale Space

---

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/scale_space_ex.jpg?raw=true)

위 사진은 Scale Space의 예시이다. Scale Space는 어떤 이미지를 하나 혹은 현재의 스케일로만 보는게 아니라 가질 수 있는 다양한 스케일의 범위를 한 번에 표현하는 공간이다. Scale Space는 가우시안필터와 이미지의 콘볼루션으로 구할 수 있다.

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/blur_image.JPG?raw=true)

L :  blur처리 된 이미지

x, y : 이미지 픽셀 좌표값

 σ : Scale Parameter

G : Gausian Filter

I : Image

![1](https://github.com/heodaewon9091/irl-study-2020/blob/master/_file/Gausian.JPG?raw=true)

단계적으로 blur되는 이미지들을 얻으려면 σ를 일정하게 높여가면 된다. σ 값을 **1/sqrt{2}**로 설정한다면 A 사이즈의 사진으로  1/(sqrt2), 1, **sqrt{2}** 배로 blur처리 된 이미지를 얻을 수 있고, B사이즈로 바꾼 후 다시 σ의 값들을 바꿔가며 얻을 수 있다. 한 사이즈의 여러 이미지들을 한 옥타브라고 정의한다.

---

<details>
<summary>참고문서</summary>
<div markdown="1">

- [Scale Space_wikipedia](https://en.wikipedia.org/wiki/Scale_space)
- [SIFT의 원리](https://bskyvision.com/21)
- [SIFT 알고리즘](https://ballentain.tistory.com/47)
- [scale space란 무엇인가](https://bskyvision.com/144?category=615305)
- [[Scale Space와 이미지 피라미드](https://darkpgmr.tistory.com/137)
- [[Pyramid methods in image processing](http://persci.mit.edu/pub_pdfs/RCA84.pdf)

</div>
</details>