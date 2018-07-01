---
layout: post
title: Tensorflow2
categories: 인공지능(AI)
---
p13
마지막 activation function을 통해서 판변이 된다는 점
두개의 layer를 하나의 matrix=
p14
weight와 bias의 계산량이 많다 -> bp사용
weight와 bias의 미분을 구한다. -> GradientDescent 가능
p21
[2,2] // 2개의 출력 , 2개입력
[2,1 ] // 2개의 입력 1개 출

코드를 읽을 수 있는 정도


딥러닝 : Deep layer
계층을 여러 개 넣을 수 있다.
hidden layer가 적은 경우는 성능이 잘 나오지만
많다면 bp로는 학습이 잘 되지 않는다 .
경사 기울기가 끝으로 갈 수록 사라짐 : Vanishing Gradient
Sigmoid는 [0..1]이라 곱하면 값이 작아진다.
ReLU max(0,x)

 RBM
 Xavier initialization
 weight 초기화

 Overfitting 해결
 Dropout
 Ensemble

 deep learning 올바른 weight 를 찾는거 ㅅ
 cnn 올바른 ㄹilter (weitght)를 찾는것
 strid 필터 움직이는 단위

 (N-F)/stride + 1
 출력 값이 작아진다 -> 정보 손실

 padding
 테두리에 0이 있다고 가정
 그립이 급격하게 작아지는 것 을 방지하고, 모서리부분이라는 것을 네트워크가 파악

 cnn에서 filter = weight
 여러 필터를 사용후 결과를 channel이라고 함 filter 개수만큼 깊이가 나온다.
 conv를 거칠때마다 크기는 작아지지만, 두께가 두꺼워짐 -> 처음 3에서 activation map의 깊이만큼

 POOLing
 두꺼운 layer에서 sampling
conv layer 후에 pooling  

사용하는 방식 위주로 공부하는게 좋을 것 같다 
