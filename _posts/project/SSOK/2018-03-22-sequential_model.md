---
layout: post
title: mlp-classifier model 생성하기
categories: project
---
{% highlight python %}
## 라이브러리
from keras.models import Sequential
from keras.layers import Dense, Dropout, Activation
from keras.wrappers.scikit_learn import KerasClassifier
from keras.utils import np_utils
from sklearn.model_selection import train_test_split
from sklearn import model_selection, metrics
import numpy as np
import json

## 단어의 총 개수 파악
word_dic = json.load(open("./data/snowe/word-dic.json"))
max_words = word_dic["MAX1"]

data = json.load(open("./data/snowe/train_data.json"))
## 데이터 읽어 들이기--- (※2)
X = data["X"] # 텍스트를 나타내는 데이터
Y = data["Y"] # 카테고리 데이터
nb_classes = len(Y)
## 출력 범주 = 필요한 카테고리 개수
batch_size = 64
nb_epoch = 20

## MLP 모델 생성하기 --- (※1)

# perceptron n개의 데이터를 가지고 0과 1로 답을 내릴 수 있는 알고리즘
# MLP 혹은 multi layer perceptreon은 여러층의 perceptron으로 이뤄진 경우를 말한다.
# 가장 간단한 Sequential 모델을 만들었다. 선형 파이프라인(스택)이다.

def build_model():
    model = Sequential()
    model.add(Dense(512, input_shape=(max_words,)))
    model.add(Activation('relu'))

# 512개의 인공 뉴런, 모든 단어만큼을 입력 형상(개수)으로 받는다
# 단어 종류만큼의 뉴런이 입력층으로 있다.
# relu: 정류된 선형 유닛, rectified linear unit으로 f(x) = max(0, x)으로 정의한다.
# => 활성화 함수의 일종, 여러 옵티마이저를 테스트하면서 신경망의 오차를 점차적으로 줄여 기본 빌딩 블록을 학습 알고리즘으로 사용한다.

    model.add(Dropout(0.5))
    model.add(Dense(nb_classes))
    model.add(Activation('softmax'))

신경망에 드롭아웃 추가
성능을 올리는 방법 중 하나로, 네트워크 내부로 전달되는 값 중 일부를 드로아웃 확률로 무작위로 제거한다 -> 잘 알려진 일반화 방법
카테고리만큼의 은닉계층을 추가한다.
마지막 계층은 활성화 함수로 softmax를 갖는다.
# metric은 목적 함수와 비슷하지만 유일한 차이점은 모델을 학습하는 데 사용하지 않고 평가하는 데만 사용
# model을 컴파일하는데 사용
# accuracy(정확도) : 타겟을 정확히 예측한 비율 -> 실제 예측이 얼마나 정확한가
# Precision(정밀도) : 참(또는 거짓)이라고 예측한 값 중에서, 실제로 참(또는 거짓)이  얼마나 있는가
# Recall(재현율) : 전체 정답에서 참이라고 예측한 것이 실제로 참인 경우의 비율
# f1 - score : 정밀도와 재현율의 평균
# 
    model.compile(loss='categorical_crossentropy',
        optimizer='adam',
        metrics=['accuracy'])
    return model

## 학습하기 --- (※3)
X_train, X_test, Y_train, Y_test = train_test_split(X, Y)
# 케라스는 데이터셋을 불러 와서 학습 데이터셋 X_train과 데이터셋 X_test로 나누고, 신경망을 미세 조정하고, 성능 평가에 사용한는 데 필요한 적절한 라이브러리를 제공한다.

Y_train = np_utils.to_categorical(Y_train, nb_classes)
# 범주 벡터를 이진 범주 행렬로 변환

print(len(X_train),len(Y_train))
model = KerasClassifier(
    build_fn=build_model,
    nb_epoch=nb_epoch,
    batch_size=batch_size)
model.fit(np.array(X_train),np.array(Y_train))
# 
# epoch : 모델이 학습 데이터를 살펴본 횟수, 각 횟수마다 옵티마이저가 가중치 조절한다.
# batch_size : 가중치 조절 전까지 살펴본 학습 데이터의 수
# 모델을 한번 밖에 안 돌렸구나....
# model.fit(np.array(X_train),np.array(Y_train), batch_size=BATCH_SIZE, epoches=nb_epoch)
# 
# 예측하기 --- (※4)
y = model.predict(np.array(X_test))
print("result: ", y)
ac_score = metrics.accuracy_score(Y_test, y)
cl_report = metrics.classification_report(Y_test, y)
print("정답률 =", ac_score)
print("리포트 =\n", cl_report)
---

# Callback : 학습 과정 데이터 관찰 용도인데, Keras Classifier의 경우 model을 h5(또는 h5py)로 바로 저장하기 까다로웠다. (다들 json이나 yaml으로 많이 저장하는 것 같았다.) 대신 Callback을 사용해서 저장된 버전을 불러서 모델 inference에 사용한다. 


check = ModelCheckpoint(MODEL, monitor='val_loss', save_best_only=False)
callbacks_list = [check]
{% endhighlight %}
