---
layout: post
title: Classification
categories: 인공지능(AI)
---
### Classification
새로운 데이터가 어떤 카테고리에 들어갈지 예측하고 분류한다.

### Decision Tree
문제와 해결방법은 tree 형태로 나타난다. 변수의 영역을 반복적으로 분할하고, 이해하기 좋기 떄문에 타인에게 설명하기 좋다. **분할 규칙(Split rule)** 에 따라 모델과 모델의 성능이 달라지고, 모델의 효율성과 성능을 위해  분할 지속이나 중단 여부(Stopping and Pruning)을 결정한다.

#### Split rule (분할 규칙)
데이터를 잘 분리하기 위해 사용할 attribute을 결정하는 규칙잉다. 여기서 '잘 분리'를 수치화하기 위해 **impurity** 라는 개념을 사용한다. impurity는 데이터 내에 얼마나 많은 그룹이 섞여 있는가를 말한다.  

### Impurity 측정
1. Chi - square statistic
분리에 사용한 attribute가 그룹을 얼마나 잘 분리했는가를 비율로 게산한 기대도수와 실제도수를 비교해서 나타낸다. 기대도수는 전체 데이터를 비율로 계산한 것이기 때문에 실제도수와 차이가 많이 날수록 잘 분리했다.
```
f(x) = (전체 데이터)*p(변수1)*p(변수2)
```

2. Gini- Index
잘못 선택 확률을 최소화하기 위한 전략으로, gini - impurity를 최소화하는 분리변수를 사욯한다.
```
f(x) = 2*p-l(good)*p-l(bad)p(left) + 2*p-r(good)*p-r(bad)p(right)
```

3. Entropy
```
Information Gain = 1 - entropy
f(parent) = p(left)
```
#### Stopping Rules
현재 node가 더 이상 분기가 일어나지 못하게 하는 규칙이다. 모든 자료가 한 그룹에 속하지 않더라도 node에 속하는 자료가 일정 수 이하이거나 impurity 의 감소향이 작을 때 그리고 depth가 일정 이상일 때 멈춘다.

#### pruning
**overfitting** 모델이 트레인 데이터에 과적합할때 오히려 일반화 성능이 떨어져 새로운 데이터에 대한 예측이 어렵다.
대안으로는 bagging(Bootstrap aggregating)이나 여러 종류의 모델을 함께 사용하는 방법이 있다. Bagging은 여러 모델을 만들어서 사용하는 것으로 1/n 데이터를 가지고 n개의 모델을 만들어 사용한다. Random forest나 ensemble model이 있다.
