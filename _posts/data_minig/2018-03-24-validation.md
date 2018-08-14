---
layout: post
title: validation
categories: data_minig
---
데이터가 예측하고 싶은 문제에 대한 정답을 갖고 있는 경우, 이 데이터는 label 값을 갖고 있다고 한다. label 값을 갖고 있는 데이터들을 그대로 학습시키고 그 모델을 가지고 예측이나 계산을 한다면, 이 모델이 정확한지 확신할 수 없다. 따라서, 모델의 정확도를 계산하기 위해 데이터를 train, 학습용과 test, 정확도 테스트 용으로 분리해서 사용한다.

#### 모형 검증
모델이 특정 데이터들을 너무 구체적으로 분류하게 되면 그 데이터들에 대한 정확도는 높아지지만, 새로운 데이터들은 분류를 할 수 없게 된다. 이를 overfitting이라고 한다.
overfitting이 발생하면 train set은 예측이 잘 되지만 test data에 대한 예측 성능이 떨어진다. 이를 해결하기 위해 validation 또는 test set을 써서 성능을 계산한다.

#### 교차 검층 (Cross Validation)
train-test set을 여러 개 사용해서 검증하는 방법이다. 여러 결과의 평균 성능과 성능 분산을 구하는게 좋다고 한다.

#### Cross-Validation
KFold 클래스를 비롯한 cross-validation 객체들은 iterator를 출력하는 split 메서드를 제공한다.
K-fold Cross-Validation는 set을 k개로 분리해서 테스트를 하는 방법이다
