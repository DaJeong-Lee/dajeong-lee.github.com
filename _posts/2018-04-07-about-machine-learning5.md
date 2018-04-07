---
layout: post
title: 모두를 위한 딥러닝(5)
date: 2018-04-07
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## 딥러닝으로 MNIST 98%이상 해보기
* 앞에서 softmax classifier 배울 때 실습했었음 -> 90% 정확도
* 뉴럴 네트워크로 구현 -> 3 layer + ReLU사용  = 94% 정확도
    > <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-10-2-mnist_nn.py>
* Xavier_initializer() 사용 = 97.8% 정확도
    > <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-10-3-mnist_nn_xavier.py>
    > 처음부터 cost가 낮음 -> 초기값이 잘 설정되었음
* 깊고 넓게 딥러닝 -> 5 layer + 중간입출력 512 = 97.42% 정확도
    * 더 깊고 넓게 모델링했는데 왜 정확도가 낮아졌을까?
    * 아마도 overfitting (너무나 학습데이터에 잘맞쳐줘서 테스트데이터의 정확도가 떨어짐)
    > <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-10-4-mnist_nn_deep.py>
    >
    > 해결책: dropout (연결의 일부를 끊어서 학습)
* Dropout 사용 = 98.04% 정확도
    > <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-10-5-mnist_nn_dropout.py>
    > 몇프로를 keep할건지 정함 (학습은 0.5~0.7, 테스팅 및 실전은 반드시 1로)
* Optimizer
    * 기존에 GradientDescentOptimizer 사용했었음
    * 다른 다양한 옵티마이져가 있음 -> 비교해본 사이트 및 논문결과 Adam이라는게 성능이 좋음
    * Use **AdamOptimizer**
* BatchNormalize: 입력값을 잘 normalize
    > <https://github.com/hunkim/DeepLearningZeroToAll/blob/master/lab-10-6-mnist_nn_batchnorm.ipynb>

-------------
## Convolutional Neural Network
* 기본아이디어는 고양이 실험: 고양이에게 그림을 보여줬더니 어떤형태의 그림을 볼때 입력을 나눠서 받음
* 이미지를 잘라서 각각의 입력으로 넘김 -> convolutional layer라고 부름
> 32*32(픽셀)*3(RGB) image 입력 -> 이미지의 일부를 우선 처리(filter 5*5*3) -> 숫자 하나만 뽑아냄 -> 어떻게?
* stride: filter를 몇칸씩 움질일건지? stride가 1이면 1픽셀씩 옆으로가면서 filter 처리
> 7*7 이미지는 3*3필터를 쓰고 stride가 1이면 출력이 5*5가 됨
* N*N 입력, Filter(F) 일때 출력은 (N-F)/stride+1
* 필터를 쓰면 값이 자꾸작아짐, 실제 사용할 때는 **padding(테두리에 0을 채움)**함
    * 그림이 작아지는 걸 방지
    * 학습시 모서리를 알려주기 위해
    * padding을 하면 7*7 넣으면 필터링 후 출력도 7*7로 나옴 -> 일반적으로 사용함
* Swiping a entire image: filter를 6개 적용(각각의 filter는 weight이 다름)
* **Activation Map**: Convolution & ReLU를 적용(swiping image)한 후 output
* **Convolutional Layer**: 여러 단계의 Activation Map을 여러번 거치는 것
    * weight의 갯수는 6, filter가 6개였으니까
* **Poorling layer**: Sampling 하는 것, 필터링 결과 6개 layer 각각 1개씩 뽑아냄 -> resize (Sampling) -> layer 쌓음 -> 6개 resize layer 생김
    * **Max Pooling**: sampling할 때 가장 큰 값을 고르는 것

## CNN case study
* AlexNet(2012)
* GoogLeNet(2014): Inception module
* ResNet(2015): 오류발생률 3.6% (사람보다 낮음)
    * fast-forward사용: layer를 점프하면서 학습하는 process가 있음
    * 왜 이렇게 하는게 학습이 잘되는지는 밝혀지지 않음
* CNN for sentence classification(2014, Yoon Kim): 텍스트를 convolutional network 사용
* Deepmind's Alpahago




