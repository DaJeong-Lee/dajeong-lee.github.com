---
layout: post
title: 모두를 위한 딥러닝(6)
date: 2018-04-09
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## RNN: Recurrent Neural Network

    Sequence Data:
    * 자연어(이전 단어들을 다 이해해야 현재 단어 이해 가능)
    * 현재 state가 다음 state에 영향을 미침

### 현재 state = function(기존 state, 입력값)

### (Vanilla) RNN: 기본적인 RNN
* RNN에서는 tanh가 잘 동작함 (sigmod 대신)
* 실습1. hello를 입력값으로 <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-0-rnn_basics.ipynb>
    * h를 입력하면 e가, e를 입력하면 l이 나오는 걸 예측하는 모델 (현재 입력값을 보고 다음 출력이 뭔지 예상)

### RNN Applications
* Language Model
* Speech Recognition
* Machine Translation
* Conversation Modeling/Qeustion Answering
> <https://github.com/TensorFlowKR/awesome_tensorflow_implementations>

