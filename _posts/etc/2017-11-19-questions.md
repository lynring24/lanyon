---
layout: post
title: 세미나 요약
categories: etc
---

## 방학 때 생각해 봤어야하는 것들
 - 기술,언어 :  kotlin / anko / re-act / dagger
 - mvvm, mvc 같은 패턴들
(물론, 서비스의 목적에 맞게 선택해야하는데, 최신 기술이라고 해서 마냥 쓰는 건 좋지 않다)

### 참고하면 좋은 자료들
>  how it feels to learn java script in 2016

### WAS
클라이언트가 아니라 서버에서 처리
single page application -> client device improved

서버가 하던 로직을 일부 클라이언트에 넘겨서 처리한다.
렌더링과 관련된건 클라이언트가 처리를 하고
모든 데이터는 api 통신을 하면서 수행을 하자.

### WEB APP
web app은 native mobile app처럼 사용 가능하게 한다.
Rails, Django를 사용하는 것 같다.
어차피 static file을 처리할거, cdn을 통해서 서비스 하자
api는 서버를 따로 구성해서 데이터만 서버와 통신하도록 하는 게 좋다.


### 다양한 블로그 포스팅
#### JAM STACK
모던 웹 개발에 대한 구성
js, api, markup
모든 동작을 프론트앤드 , 서버단 처리는 재사용 가능한 api로 추상화 , markup static site generate할 때 많이 사용
jekyll 등

static site generator 블로그, 회사 홈페이지 등
운영이 쉽고, content와 code의 분리
탬플릿 엔진 기반

jam stack? 성능이 좋다. cdn을 통해 배포가 가능하므로
django로  만들고 띄우면 latency 차이가 줄어들고, cost가 줄어든다 (서버, 운영비,보안 )
클라이언트에는 중요데이터가 나갈수없기 때문에 보안이 중요하다

cdn에 업로드가 가능해야하고
배포시 캐시는 즉시 폐기
배포는 모든 변경 파일이 업로드 완료기에 적용
git으로 관리를 하고
모던 빌드 도구 활용
빌드 자동화 마트업 변경사항을 실시간으로 확인 가능하게

#### Nelify?
Github pages : 깃허브제공. static web site를 무료로 호스팅 가능하게 -> github.io.domain
저 도메일을 사용하고 싶지 않을 떄 custom domain으로 수정이 복잡하다.
jekyll을 지원.
branch에 대한 제한이 있다.
ghpages, main 등 옵션으로 브랜치에 대한 제약이 있다.

#### CloudFlare
CDN 이자 ddos 방어, dns 서비스도 가지고 있다.
가지고 ㅣㅆ는 돔메일 서비스 권한을 넘기고, 도메일을 알아서 붙여줘서 다 처리해줌
개인 도메일이 필요하다 .

#### Nelify
JAM STACK 호스팅 제공을 해준다. 무료, 전세계 cdn
개인 도메인이 필요하다.
장점 : github + CloudFlare 의 기능을 모두 가지고 있어서 처리해준다.

#### AWS S3 + CloudFlare
web publishing 지역성이 있다.
도메인에 대한 권한을 아마존에게 넘겨야한다.
