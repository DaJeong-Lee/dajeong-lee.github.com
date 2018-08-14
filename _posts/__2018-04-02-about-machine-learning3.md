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
* Axis: 배열 바깥쪽이 0, 안쪽 차원으로 들어갈수록 +1씩 증가 (-1은 제일안쪽)
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
    각각은 logistic function f(x) = wx * b
   [x1]
   [x2] => [y1]
                 => [y']
   [x1] => [y2]
   [x2]

   맞는 W와 b가 주어졌다고 가졍하면 xor를 풀 수 있음
   -> 그러나, 맞는 W와 b를 찾아내기가 매우 힘듬
   -> 이걸 구하기위해 back-propagation 알고리즘 등장
   -> 끝까지 계산한다음에 틀리면 끝에서부터 앞으로 돌아가면서 계산함
</pre>

## 미분 정리하기
* 미분은 순간변화율을 구하는 것 = 기울기
> f(x) = 3, 상수를 미분하면 0
>
> f(x) = 2x = x + x 를 미분하면 2
>
> f(x) = x+3 을 미분하면 (x 미분값 1 + 상수3 미분값 0) = 1
* 편미분: 미분대상을 뺀 나머지는 상수로 보고 미분함.
* **chain rule**: f(g(x))를 x로 미분-> 델타f/델타g (밖에꺼미분) * 델타g/델타x (안에꺼미분)

## Nueral Network로 XOR 문제 해결
* x1, x2 값을 주고 xor 연산의 결과값을 예측하는게 목적!

* xor 연산 모델이 틀리지 않았슴에도 틀린결과가 나옴 -> nueral network 연산 필요
> [실습 source](https://github.com/DaJeong-Lee/tensorflow) xor.py
* xor 연산 2개 연결시키니까 잘됨
> [실습 source](https://github.com/DaJeong-Lee/tensorflow) xor_nn.py
* xor 연산을 여러개 깊게(옆으로뿐만아니라 밑으로도) 연결시키니까 더 학습 잘됨 (deep neural network)
> [실습 source](https://github.com/DaJeong-Lee/tensorflow) xor_nn_wide_deep.py

## TensorBoard: 학습을 길고 복잡하게 할때 진행상황을 한눈에 볼 수 있게 도와줌 -> 그래프로 보여줌
> [실습 source](https://github.com/DaJeong-Lee/tensorflow) xor_tensorboard.py
>
> 명령어 tensorboard --logdir=./logs/xor_logs_r0_01
>
> localhost:6006으로 접속하면 그래프 볼 수 있음

* learning_rate 값을 변경해가면서 비교해서 볼 수 있음


