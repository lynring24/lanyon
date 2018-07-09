---
layout: post
title: Framework Caffe와 solver
categories: 인공지능(AI)
---

**From http://caffe.berkeleyvision.org/tutorial/solver.html**

### Solver 
Solver는 model optimization으로  parameter를 조정하면서 loss를 개선한다. 모델의 학습은 Solver와 Net으로 나뉘다. Solver는 optimization과 parametergenerate을, 
Net은 loss와 gradient를 산출한다. 

#### Type
+ Stochastic Gradient Descent 
+ AdaDelta
+ Adaptive Gradient
+ Adam
+ Nesterov's Accelerated Gradient
+ RMSprop

### Stochasitc gradient descent (SGD) 
SGD는 linear combination과 이전 weight을 반영해 weight W를 업데이트한다. Learning rate α는 negative gradient의 weight이다.
The momentum μ은 이전 update의 weight이다. 
```
Vt+1=μVt−α∇L(Wt)
Wt+1=Wt+Vt+1
```
### AdaDelta
AdaDelta method is a robust learning rate method. SGD처럼 gradient-based optimization이다. 
