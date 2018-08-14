---
layout: post
title: 모두를 위한 딥러닝(4)
date: 2018-04-03
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## Sigmod 대신 ReLU
* 뉴럴 네트워크에서 sigmod역할 function을 activation function이라고 부름

#### Backpropagation 알고리즘의 문제점
* Backpropagation 알고리즘은 2~3개는 잘 학습되는데 9개, 10개 같이 딥러닝은 학습이 잘 안됨
    * 각 단계별로 sigmod가 붙어서 단계별 출력값이 1보다 작음 -> 단계별 곱셈 -> 단계가 지날수록 더 작아짐
    * Vanishing gradient(경사로가 사라지는 문제): 단계가 너무 많아서 결국 맨 앞에 W가 0.00000001 같이 아주 작아져버림
    * 맨 앞에 입력값이 맨 뒤 출력값에 미치는 영향이 아주 아주 작음 -> 큰 문제

#### ReLU(Rectified Linear Unit): 0보다 작으면 0, 0보다 크면 직선으로 위로 감

**뉴럴 네트워크에서는 sigmod 대신 ReLU를 사용** (마지막 단계만 sigmod 사용)

#### Leaky ReLU, Maxout, ELU: 0보다 작을 때 0이 아닌 아주 작은 값으로 내려가도록
#### tanh: sigmod의 수정판

----------------
## Weight 초기값 잘 정하기
* RBM(Restricted Boatman Machine): 지금은 많이 안쓰지만 알아두면 좋을듯
* Xavier initiallization: ,2010
* He initiallization: ,2015
* MSRA
> 잘 구현해놓은 코드가 있으니 갖다쓰면됨

----------------
## Dropout과 앙상블
* overfitting 인지 구분하는법
> 학습데이터의 정확도는 높은데, 검증데이터의 정확도는 낮은 경우 -> overfitting
* 깊게 뉴럴 네트워킹 될수록 오버피팅 될 확률이 증가함

### overfitting 솔루션
* 많은 학습데이터 사용
* Regularization
    * 너무 큰 weight은 주지말자 -> 그래프를 좀 평평하게 펴자
* Dropout (2014): 뉴럴네트워크의 몇개 노드 연결을 끊어버림 (랜덤하게)
> 랜덤하게 노드를 pass해가면서 훈련 -> 나중에 총 동원해서 예측하면? -> 왜 그런지 아직 모르겠음
>
> 주의할점: 학습할 때만 빼고, 실제 평가/사용 할 때는 모든 노드를 연결

### Ensemble(앙상블)
* 똑같은 형태의 딥러닝 n개를 만들고, 각각 학습시킴 -> 맨 마지막에 합침
* 실제 해보면 2% ~ 5% 정도의 성능 향상이 있음

-----------------
## 레고처럼 네트워크 모듈 쌓기
* Feedforward neural network: layer를 직렬로 쭉 쌓기
* Fast forward: layer를 두단계씩 뛰어넘으면서 더해줌
* Split & merge: 나눠서 가다가 합치고 나눠서 가다가 합치고 하는 구조
* Recurrent network (RNN)











