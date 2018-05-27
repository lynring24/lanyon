---
layout: post
title: Regression - Linear regression
categories: 인공지능(AI)
---
## Linear regression
들어오는 인풋이 이전에 정의된 데이터 포맷과 같은 패턴을 가질 것이라고 가정하여 수치를 예측하는 방식. model의 형태가 linear combination이다.  

### 측정 방식
1. Least Squares Estimation<br>
오차 제곱의 합이 최대가 되는 평가 함수를 찾는다.  오차의 합이 아니고 굳이 제곱을 사용하는 이유는 (3이상 승수를 사용해도 상관은 없다) 유일 해와 미분을 하기 위함이다. 단순하지만, 데이터가 증가하면 계산량이 많아진다.
```
hθ(x) = θ0 + θ1*x
j(θ) = (1/2*m) * Σ (i=1..m) (hθ(xi)-yi)^2
m = data set size
minimizeθ j(θ)
```

2. Maximum Likelihood Estimation
확률 개념 새용, 결과가 나올 가능성을 최대로 만드는 parameter를 찾는다.
동전을 10번 던질 떄 앞면이 7번 나올 가능성을 최대로 만들는 파라미터는
```
L(θ|7F , 3B) = p(F)^7 + (1-p(B))^3 = θ^7 + (1-θ)^3
```

3. Gradient Descent
파라미터를 대입해가면서 수렴할 때까지 반복하는 방법이다. global optimum은 보장하지 않지만, local optimum은 보장한다.
```
repeat until convergence {
  θj = θj - α*(∂*j(θ)) / ∂*θj
}
```
### 다중선형회귀와 다항회귀
<table>
<tr> <td> 다중선형회귀 </td> <td> 다항회귀 </td> </tr>
<tr> <td> 모델 파라미터 여러 개 </td> <td> 항의 차수가 2 이상</td> </tr>
</table>
