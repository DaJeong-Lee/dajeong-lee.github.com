---
layout: post
title: 모두를 위한 딥러닝(3)
date: 2018-04-02
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## 딥러닝의 기본개념
* 기존에 **뉴럴 네트워크**라고 불린 알고리즘(몇십년간 실패ㅠㅠ)을 새롭게 **딥러닝**이라고 부름(Breakthrough in 2006,2007 by Hinton and Bengio)

## Tensor Manipulation

### Array(Tensor)
* Rank: 몇차원 array인가?
* Shape: elements가 몇개? # [[1,2,3],[3,4,5]] 의 shape은 (2,3)
* Axis: 배열 바깥쪽이 0, 안쪽 차원으로 들어갈수록 +1씩 증가
* Maxtrix 곱을 할 때 shape이 맞아야 함
* maxtrix 곱(matmul(mat1, mat2))과 그냥 곱하기(mat1*mat2)는 결과가 완전히 다름

#### BroadCasting: shape이 달라도 연산할 수 있게 해주는것
    * 주의 해서 사용할 것
    * 계산하는 matrix랑 shape을 맞춰줌 [3]을 [[3,3]]으로 만듬

* ### reduce_mean(): 평균을 계산하는데 줄여서 계산해줌
    * integer넣으면 뒤에 다 짜름.. -> 꼭 **float**으로 계산할 것
<pre>
<code>
    x = [[1., 2.],
         [3., 4.]]

    tf.reduce_mean(x).eval() # 축이 없으면 전체 평균
    #result: 2.5

    tf.reduce_mean(x, axis=0).eval() # 축0은 배열 바깥쪽 (1,3)의 평균 (2,4)의 평균
    #result: [2., 3.]

    tf.reduce_mean(x, axis=1).eval() # 축1은 배열 안쪽 (1,2)의 평균 (3,4)의 평균
    #result: [1.5, 3.5]

    tf.reduce_mean(x, axis=-1).eval() # 축-1은 배열 제일 안쪽 (1,2)의 평균 (3,4)의 평균
    #result: [1.5, 3.5]
    #가장 많이 사용하는 축: -1
</code>
</pre>

* ### reduce_sum(): 합을 계산하는데 축으로 계산가능
    * axis -1을 제일 많이 씀(제일 안쪽 축)

* ### argmax(): maximum 값의 위치(index)를 구하는데 축으로 계산가능

* ### **Reshape**: 원하는 형태로 shape을 바꿀 수있는 fucntion
    * 보통 사용할때는 가장 안쪽축은 그대로 두고 밖을 바꾸는 형태로 씀
* #### squeeze: [[1],[2],[3]] -> squeeze -> [1,2,3]
* #### expand_dims: [1,2,3] -> expand_dims 1 -> [[1],[2],[3]]

* ### One hot: 3 -> 000100 (index 3만 1로 줌)
    * one hot을 하면 자동으로 dimension이 1 추가됨

* ### Casting: 데이터 자료형을 바꿈 integer -> float

* ### Stack: array x,y,z를 [x,y,z]로 쌓아줌
    * axis를 바꿈으로 shape을 변경할 수 있음

* ### ones_like(): 주어진 shape과 똑같은 1이 들어있는 tensor를 만들어줌
* ### zeros_like(): 주어진 shape과 똑같은 0이 들어있는 tensor를 만들어줌
* ### zip(): python 함수

## 뉴럴 네트워크로 XOR 문제 풀기

* multiple logistic regression을 사용
* XOR: exclusive OR -> 두개의 값이 다르면 1, 같으면 0

### 3개의 nueral network로 풀기
<pre>
   [x1]
   [x2] => [y1]
                 => [y']
   [x1] => [y2]
   [x2]
</pre>









