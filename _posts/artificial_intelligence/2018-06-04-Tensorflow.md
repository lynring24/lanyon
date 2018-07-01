---
layout: post
title: Tensorflow
categories: 인공지능(AI)
---
tensor : 데이버 배열 -> 엣지로 표현
node : 연산 및 변수로

tf.constant : constant 형성 -> constant 노드 형성
constant node
tf.constant(VALUE, TYPE)
tf는 세션을 형성하고 실행을 해야 결과를 받을 수 있다. 그 전까지는 그냥 객체
{% highlight python%}
session.run();
{% endhighlight python %}
매번 세션(session)을 생성 해주어야 한다.

# Mechanism
1. 그래프 빌드
2. run
3. return

### placeholder
tf.placeholder( TYPE );
feed_dict : 각 노드에 값을 넣어준다. 타입은 리스트 형도 가능하다.

## Tensor : n 차원의 array
1. rank : 배열의 차원 (선형대수의 개념과 동일)
2. shape : 배열의 모양 (nxm==[n,m])
3. TYPE

# Linear Regression
**Variable 노드** : 텐서플로우가 학습하는 과정에서 자체적으로 변경시키는 값
1. build model
{% highlight python%}
tf.Variable(shape, name);

cost = tf.reduce_mean(tf.square(hypothesis - t_train));
optimizer = tf.train.GradietDescentOptimizer(learning_rate=0.01)
train = optimizer.minimize(cost)
{% endhighlight python%}

2. session and build model
{% highlight python%}
sess = tf.Session()
sess.run(tf.global_variable_initializer())

for step in range(2000):
  session.run(train)
  if step % 20 ==0:
    print(step, session.run(cost), sess.run(W), session.run(b))
{% endhighlight python%}

## placeholder
{% highlight python%}
x_train = [1,2,4]
x = tf.placeholder(tf.float32, shape=[None]) # not fixed, 여러개
{% endhighlight python%}

## Matrix
{% highlight python%}
x_date = [[],[1,2,3],[1,2,3], ..]
shape=[None, 3] # nx3 Matrix
weight = [feature 수, 출력값 수]
bias = [1]
tf.matmul() # Matix 곱 연산
{% endhighlight python%}

#### loading data from file
{% highlight python%}
import numpy as np

xy = np.loadtxt();
x_data = xy[:, 0:-1]
y_data = xy[]
{% endhighlight python%}

#### Queue runners
파일이 커서 메모리에 올리기 어려운 경우 -> 큐를 제공한다.
