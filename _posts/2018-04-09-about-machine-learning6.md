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

## RNN Basics

#### 실습
1. cell을 만든다. num_units: 출력의 크기를 정함(hidden_size)
>  cell = tf.contrib.rnn.BasicRNNCell(num_units=hidden_size)
2. 셀 구동, _states는 마지막 스탭의 state
> outputs, _states = tf.nn.dynamic_rnn(cell, x_data, dtype=tf.float32)

##### 셀 생성과 구동을 따로 하는 이유는 원하는 형태의 셀을 바꿀 수 있기 때문
> BasicRNNCell을 BasicLSTMCell로 바꾼다던지, GRUCell로 바꾼다던지..

##### <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-0-rnn_basics.ipynb>
* 입력을 one hot encoding으로
> input data의 dimension이 (3,5,4)인 경우, 3은 batch_size 5는 sequence_length(몇번 실행되는지) 4는 one hot encoding bit 갯수
>
> hello를 입력데이터로 쓰면 실행을 4번하니까 sequence_data는 4가 됨 (h->e, e->l, l->l, l->o)
>
> 문자열은 hello, eolll, llell 3개의 문자열을 주면 batch_size는 3이 됨
* 출력 dimension은 개발자 마음대로.. -> 셀 생성 시 hidden_size를 뭘로 했는지에 따름
> output data의 dimesion이 (3,5,2)인 경우, 3은 batch_size 5는 sequence_length 2는 hidden_size
>
> 출력은 weight들, 출력의 shape을 보기위해 print 해본것

## RNN - hihello Trainning
<https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-1-hello-rnn.py>
* 어떤 문자 다음에 올 문자가 무엇일지 예측하는 모델
    * h다음 i가 올지 e가 올지는 그 앞에 데이터를 봐야함으로 RNN을 써야함
> sequence_loss = tf.contrib.seq2seq.sequence_loss(logits=outputs, targets=Y, weights=weights): 정확도 측정, 정확도가 높을수록 loss값이 낮음
>
> 사실 rnn의 output을 바로 logits로 사용하면 안좋음 -> 실습에서는 간단하게 하려고 이렇게 함

## Long sequence RNN
<https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-2-char-seq-rnn.py>
* sample(입력값)만 바꾸면 자동으로 메타데이터들이 들어가도록 만듬
* 굉장히 긴 문자열을 입력값으로 주면?? -> 문자열을 잘라서 batch를 만듬(sequence_length 갯수로 자름)
* 실제 돌려보면 잘 안됨 ㅠㅠ -> logits, 얕은 RNN이 문제

## Stackted RNN + Softmax Layer
<https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-3-char-seq-softmax-only.py>
<https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-4-rnn_long_char.py>
* Wide & Deep RNN 사용 -> Stacked RNN -> rnn.MultiRNNCell()을 사용(몇개를 쌓을것인지 *N)
* 맨 마지막에 Softmax를 붙여줌
    * RNN output을 reshape -> softmax input으로 씀

## Dynamic RNN
* 가변하는 sequence를 입력으로 받기 위해 사용
* tf.nn.dynamic_rnn()의 parameter sequence_length를 각각 다르게 주면 됨

## RNN with time series data
<https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-12-5-rnn_stock_prediction.py>
* time series data: 시간에 따라 값이 변하는 데이터(주식가격, )




