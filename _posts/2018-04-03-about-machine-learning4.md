---
layout: post
title: 모두를 위한 딥러닝(4)
date: 2018-04-02
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

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


