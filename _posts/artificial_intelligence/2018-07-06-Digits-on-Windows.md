---
layout: post
title: Digits on Windows 윈도우에 digits 설치하기
categories: 인공지능(AI)
---

Digits를 윈도우에 설치할 사람은 지금이라도 리눅스를 사용해서 깔길 추천한다. <dir>
세상에 이렇게나 복잡한 설치 과정이 있을 줄 몰랐다. 
> 물론 내가 버전 제대로 확인하지 않고 무대포로 진행한 문제도 있긴 하지만! 대체 설치가 복잡하고, 윈도우 설치에 대한 자료들은 다 오래되서 업데이트도 안 되어 있다. 

## 설치해야하는 프로그램들 
1. Python2
2. CUDA 7.5
3. CuDNN 5.1
4. Caffe 
5. Graphviz
6. Viusal Studio 2013/2015(컴파일러)

> 사용하는 컴퓨터의 성능과 옵션에 따라서 사용 가능한 버전이 달라진다. 내가 사용한 컴퓨터는 GPU가 없어서 버전을 올릴 수가 없었다. 


## 설치 과정 
Caffe 설치 전까지는 아래의 문서를 따라서 설치하면 된다. <dir>
https://github.com/NVIDIA/DIGITS/blob/820c82f257233845f21a9ef2addd84d3c59cf006/docs/BuildDigitsWindows.md<dir>

### Caffe 설치와 고생길
Caffe 설치 때문에 이틀을 고생했다. 일단 자료가 옛날 자료라서 최신 버전 Caffe에 없는 파일들을 수정하라고 나온다. (이것 때문에 clone만 n번 했다.)
설치하려는 사람들은 제발 버전을 무시하는 실수를 하지 않았으면 좋겠다. 


+ caffe 설치 시 경로에 **공백이 있으면 안 된다**.
+ 환경변수는 생각보다 늦게 반영된다. 

###### 참고한 블로그 
+ http://baemincheon.tistory.com/21
정리를 깔끔하게 해두신 글이었다.

#### GPU가 없어서 CPU_ONLY 옶션을 사용해야 할 때 
손본 파일

+ Makefile.config
+ scripts\build_win.cmd
+ Makefile 

Makefile.config.example이라는 파일이 있을텐데, 복사해서 Makefile.config를 만들고 옵션을 변경해야 한다. 위에서 언급한 파일들에 CPU_ONLY를 전부 1로 바꿨더니 된것 같다

### Digits 설치와 고생길
+ requirement.txt를 돌리고 싶었지만 이미 설치된 버전은 첫 단추부터 글러먹어서 일일이 설치했다. 
+ python -m digits 서버를 여는 주문이다. 
+ localhost:5000 서버를 여는 주문2

#### 신나게 겪은 에러와 버그들 
#####  파이썬 2.7과 2.7.15는 또 다르다.
파이썬 3.x와 파이썬 2.x가 호환 안 된다는 것은 여러 삽질을 통해서 이미 겪어 왔지만, 2.7과 2.7.15가 또 다르다는 걸 몸으로 익혔다. 
##### cannot open include file 'caffe/include symbols.hpp' no such file or directory
https://github.com/BVLC/caffe/issues/5840 <dir>
헤더 파일 중에 include_symbol.hph가 자동으로 연결되는게 아니어서 복붙 했어야했다.
##### pydot은 버전이 바뀌면서 graphviz가 없다
검색해보니 원래 있다 없어졌다고 하는 사람들도 있고, pydot-ng를 설치하라는 사람도 있었다. 
확인해보는 결과 원래 그냥 없고, 대신 pip install pydotplus를 하세요.
##### IOError: [Errno 2] No such file or directroy: ‘C:\programs’
program files 가 짤린 것이라고 예측해서 Digits 폴더의 위치를 C의 최상위로 옮겼다. 
경로에 공백이 들어가면 경로 인식이 안 된다.
##### Unable to load any image from file PATH_TO_TRAIN_FILE_LIST.txt
MNIST를 그래도 사용하는 경우, 파일을 열어보면 경로랑 카테고리가 같이 들어있어서 경로 인식이 안 된다. 경로만 따로 뽑아야 한다. 
##### 브라우저가 다른 탭을 여는 바람에 크롤링이 안 되는 경우
모델 생성부터 성능까지 처리하는 크롤러를 만들었는데, 탭이 열리는 문제가 발생했다. 
{% highlight python%}
button = browser.find_element_by_css_selector('#test-model-form > div:nth-child(4) > div:nth-child(2) > button:nth-child(5)')
browser.execute_script("arguments[0].setAttribute('formtarget','_self')", button)
{% endhighlight python%}
js, html,css 속성 target을 "_blank”에서 ‘_self’로 수정했다. 
