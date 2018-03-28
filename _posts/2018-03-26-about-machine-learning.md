---
layout: post
title: 모두를 위한 딥러닝(1)
date: 2018-03-26
description:
tags:
---

# 모두를 위한 딥러닝(1)
##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## 기본적인 머신러닝 개념설명
* 머신러닝: 학습하는 프로그램
* supervised learning: 정해져있는(label이 달려있는) 데이터를 가지고 학습
	* 0~100점 같은 넓은 범위를 예측하기 위해 사용: **regression**
	* Pass/Non Pass 2가지로 나눌경우 사용: **binary classification**
	* A,B,C 같은 grade를 줄 때 사용: **multi-label classification**
* unsupervised learning: label이 달려있지 않은 데이터를 가지고 학습
* trainning data set: 학습을 위해 필요한 label이 있는 데이터

## TensorFlow 기본
 - 구글에서 제공하는 머신러닝 open source library
 - numerical computing using data flow graphs
 - data flow graph란 node와 node를 연결하는 edge가 있고, node들이 어떤 operation이고, edge는 data arrays(tensors)이고, data arrays들이 node를 돌아다니면서 계산되는 것.
* 설치
> pip install tensorflow

1. bulid graph (constant or placeholder)
2. session.run()
3. update variables in the graph

* Tensor는 data array를 의미
    * ranks: 몇차원 array인가? ( 0 -> n 까지 )
    * shapes: 각각 element에 몇개씩 들어있는가? ( [1,2,3].[3,2,1] 은 shape [2,3] )
    * data types: 대부분 float32, int32

## Linear Regression
> regression: 0~100 범위값을 구하는 학습 ( 몇시간 공부하면 몇점을 받을 수있을까? 입력값 x는 시간 에측값 y는 점수 )

#### Linear Hypothesis(선형 가설): x값이 커질수록 y값도 커짐, H(x)=Wx * b (일차방정식)
#### Cost function: 세울 가설 H(x)와 실제 데이터가 얼마나 다른가를 나타냄
> 얼마나 다른지 차이를 계산하는 방법(Cost function): (H(x) - y)^2
차이가 작으면 낮은 값(칭찬), 차이가 크면 높은 값(벌)을 줌.

Cost function은 Cost(W,b) W와 b의 function임.
-> 이를 위한 많은 알고리즘이 존재함.
-> Cost function을 통해 Cost가 제일 작은 W와 b를 찾는게 학습목표임.

* [실습 source](https://github.com/DaJeong-Lee/tensorflow) linear_regression.py

### cost(W) 최소화 알고리즘
* Gradient(경사) descent(내려감) algorithm: 경사도를 따라 내려가면서 최소값을 찾음
> cost(W)에서는 W값을 조금씩 바꿔보면서 최소값을 찾음 -> 항상 최저점에 도착할 수 있다!
>
> 주어진 그래프에서 경사도구하기 ->  미분
    * Convex function: 밥그릇 엎어놓은 모양의 그래프 -> 우리의 가설 cost(W)는 이런모양임 -> 어디서 시작하든 같은 최소값을 가짐
* [실습 source](https://github.com/DaJeong-Lee/tensorflow) linear_regression_cost_min.py

## Multi-variable linear regression
* 여러개의 입력값으로 결과값을 에측하기 위해 사용
* Hypothesis: H(x1,x2,x3) = w1x1 + w2x2 + w3x3 + b
* Matrix multiplication(행렬 곱셈) -> 위의 식을 행렬로 표현 (x1, x2, x3) * 세로(w1,w2,w3) =위의 식과 같음 -> H(X) = XW (대문자는 행렬을 의미, X를 먼저써야 행렬곱으로 계산가능)
* hypothesis using matrix:  5행3열 [5,3] * [3,1] = [5,1] 앞에 3끼리 값아야 곱셈가능하고, 곱셈결과는 3을 제거한 [5,1]임
* X [5,3] * W [?, ?] = H(X) [5,1] 일 때 ?를 구하면? -> [3,1]
> 참고: 1e-5는 0.00001, 1e5는 100000
* [실습 source](https://github.com/DaJeong-Lee/tensorflow) multi_variable_regression.py

### Queue Runners: 텐서플로우에서 제공하는, 메모리가 작아도 데이터를 계산할 수있는 모듈
* 여러 파일에서 읽어서 queue에 쌓아놓고 reader -> decoder -> queue에 쌓음

## Logistic classification
### binary classification: 두개 중 하나로 예측 -> ex) email이 스팸인지 아닌지?

### Hypothesis function
* logistic function(sigmoid function): x가 커지면 1에 가까워지고, x가 작아지면 0에 가까이가는 s모양 함수 -> g(Z) = 1 / (1 + e ^ -Z)
* hypothesis가  Z = WX 라고 할때, H(x) = g(Z)(sigmoid function에 Z값 넣은 결과값) 라고 둠.
* logisction classification의 Hypothesis = 1 / 1 + e ^ -WtX

### Cost function
* logistic function의 cost function은 구불구불한 밥그릇 엎어놓은 모양 -> Gradient Descent Algorithm 사용불가능 -> 기울기가 낮다고 최저점이 아님. 일정 시점후 또다른 최저점 존재할수도..
#### New Cost function
* H(x)에 제곱이 있어서 구불구불하니까 그걸 log를 써서 상쇄한다는게 기본생각이고, 실제 log함수의 모양을 보면 X값 변화에 따라 0,무한대에 가까워지므로 classification이랑 잘맞음.
    * 예측실패시(1) cost는 큰값, 예측성공시(0) 0으로 수렴하므로 classification에 쓰기적당함. -> 매끈한 밥그릇 모양 cost function이 나옴 -> Gradient Descent Algorithm 쓸 수있음

#### Minimized Cost function
* Gradient Descent Algorithm 적용해서 최소값 구하기
* 참고. <https://www.kaggle.com>에 많은 데이터 있음
* [실습 source](https://github.com/DaJeong-Lee/tensorflow) logistic_classifier.py



