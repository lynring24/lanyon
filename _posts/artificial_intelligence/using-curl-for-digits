---
layout: post
title: Curl로 Digit 돌리기
categories: 인공지능(AI)
---
# Curl과 Digits
localhost로 브라우저로 Digits를 사용할 수 있는데 굳이 curl을 사용하는 이유는 crawl을 하기 시작했더니 터무니없이 느려진 속도 때문이다.
Digits는 train data set에 대한 결과는 나오지만 test data set에 대한 결과가 나오지 않는다. ~~버전에 따라 있다는 이야기도 있던데 찾다가 포기했다.~~
그래도 배워둔게 있다고 test data set에 대한 결과를 측정해보고 싶어서 crawler를 만들었다. 모델 빌드부터 결과까지 돌려서 가져오게 했는데, 마지막에 test data 
결과를 긁어오는게 너무 느려서 포기하고 cmd창에서 curl로 돌리기 시작했다. 

<code>
# 로그인
curl localhost:5000/login -c digits.cookie -XPOST -F username=USERNAME

# Train data set 만들기
curl localhost:5000/datasets/images/classification.json -b digits.cookie -XPOST -F folder_train=D:\MINST\train -F encoding=png -F resize_channels=1 -F resize_width=28 -F resize_height=28 -F method=folder -F dataset_name=mnist_dataset
curl localhost:5000/datasets/20180706-111701-2e5b/status

# 결과
curl localhost:5000/index.json
curl localhost:5000/models/20180706-111701-2e5b.json

# server direcroy 
C:\Digits\digits\jobs\20180706-111701-2e5b

# create model 
curl localhost:5000/models/images/classification.json -b digits.cookie -XPOST -F method=standard -F standard_networks=lenet -F train_epochs=30 -F framework=caffe -F model_name=lenet_base -F dataset=20180706-111701-2e5b
job_id = '20180706-115037-2f35'
curl localhost:5000/models/20180706-115037-2f35.json

# classificaion
curl localhost:5000/models/images/classification/classify_many.json -XPOST -F job_id=20180706-115037-2f35 -F image_list=@D:\MINST\Extraction\extracted.txt > predictions.txt

# model description
curl localhost:5000/datasets/20180706-170647-78f1.json

</code>
