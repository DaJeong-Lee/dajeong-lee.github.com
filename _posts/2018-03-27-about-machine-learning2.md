---
layout: post
title: 모두를 위한 딥러닝(2)
date: 2018-03-27
description:
tags:
---

# 모두를 위한 딥러닝(1)
##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## MachineLearning 실용과 팁

### learning rate 정하기
* gradient descent algorithm 사용할 때 learning rate를 잘 정하는게 중요
* learning rate: 경사면을 따라 내려갈 때 얼만큼 내려가는지에 대한 값
* overshooting: learning rate가 너무 커서 계속 최소값을 못찾고 튕겨나가는 현상(cost함수 발산)
* learning rate가 너무 작으면 연산하다 시간이 다되버려서 최저점이 아님에도 스톱될 수 있다.
* 처음에는 0.01로 learning rate를 출력하면서 cost를 보고 너무 작게 변하면 조금씩 올리면서 해보면 됨

### Gradient descent altorigthm을 사용하기 위해 X 데이터 전처리
* zero-centered-data: 데이터의 분포를 보고 데이터의 중심이 0으로 이동하도록
* normalized-data: 값의 범위가 어떤 범위에 항상 들어가도록 변경하는 것
    * 데이터가 너무 크거나 들쭉날쭉할 때는 꼭 normalize를 해줘야함
* normalization은 여러가지 방법이 있는데 그 중 1개가 standardization
> standardization은 파이썬 코드 한줄로 가능: 변환된 x값 = x값을 평균으로 빼고, 분산으로 나눔
>
> tensorflow에서는 MinMaxScaler(xy)사용: 0과 1사이로 데이터를 변환함

## Overfitting: 학습데이터에만 너무 잘맞는 모델을 만드는 문제, 그래프를 보면 많이 구부러져있음(학습데이터에 맞도록)
* 학습데이터에 너무 잘 맞는 모델을 만들었는데, 테스트 데이터나 실제 데이터를 넣으면 잘 안맞는 경우가 생김
* 해결방법
    * 학습데이터를 많이 갖고있거나
    * 중복된 데이터를 제거
    * Regularization

### Regularization
* 너무 큰 weight를 주지 말자(그래프를 구부리지말고 펴자)
* cost function에 lamda(regularizaiton strength * W^2의 합) 을 더해줌
* tensorflow에서는 아래와 같이 구현
> l2reg = 0.001 * tf.reduce_sum(tf.square(W))

## Trainning / Testing 데이터 셋
* 갖고 있는 데이터를 **trainning set, test set**으로 나눠서 사용할 것
* trainning set으로 모델을 만들고 학습을 시키고, 평가할 때 test set을 사용
* trainning set을 trainning set과 **validation set**으로 나눠서 validation set으로 **learning rate, regulation의 lamda값**을 모의실험해서 최적값을 찾음

## Online learning
* 한번에 메모리에 데이터를 다 넣어서 학습시키기 어려움
* 학습데이터가 100만개가 있다면 10만개씩 잘라서 학습시키려면 학습된 결과가 계속 남아있어야함

## MNIST Data set으로 실습
* 손으로 쓴 우편번호를 구별하기 위해 만들어진 데이터셋
* 28*28 총 784개 픽셀에 번호가 적혀있음(x), 결과는 0~9(y)
* tensorflow에서 데이터를 제공해줌
* epoch: 전체 데이터셋을 한번 학습시킨것을 1 epoch이라고 함 (100개 데이터셋이 있고 batch size가 10일때, 1 epoch 완성하려면 10 loop을 돌아야함)




