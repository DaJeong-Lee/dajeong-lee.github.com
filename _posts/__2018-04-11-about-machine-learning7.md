---
layout: post
title: 모두를 위한 딥러닝(7)
date: 2018-04-11
description:
tags:
---

##### [인프런 - 모두를 위한 딥러닝 강좌](https://www.inflearn.com/course/%EA%B8%B0%EB%B3%B8%EC%A0%81%EC%9D%B8-%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-%EB%94%A5%EB%9F%AC%EB%8B%9D-%EA%B0%95%EC%A2%8C/)

## Tensorflow를 AWS에서 돌려보자
* 윤석찬님 자료 보기
* EC2 인스턴스 생성 - GPU Instance 선택 - Add Storage(12GB)
* CUDA, cuDNN 설치 후 tensorflow 설치(gpu버전)
* GPU 사용여부에 따른 속도 -> 대략 25배 정도? (mac vs AWS)
* Spot Instances: 놀고있는 서버를 사용(가격이 더 쌈)
    * 경매에 참여해서 서버를 입찰받아야 됨
* 사용하지 않는 EC2는 항상 Stop 해야함(돈이 안나가도록)
    * Cloud Watch : cpu의 부하여부에 따라 서버를 내릴 수 있음
    * 학습 후 서버 shutdown 코드를 파이썬에 추가하는 것도 좋은방법

## Google Cloud ML
* tensorflow task를 클라우드에서 실행


