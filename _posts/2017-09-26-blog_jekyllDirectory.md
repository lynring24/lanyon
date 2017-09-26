---
layout: post
title: jekyll
categories: Blog
---

jekyll을 모르고 블로그를 커스텀하려니까 막막한데, 사실 문서를 봐도 딱히 와닿지 않아서 야매로 정리해봤다.

# jekyll의 디럭토리 구조
`.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid YAML Frontmatter`

+ config.yml : blog의 전체적인 구성을 담고 있는 파일. 안드로이드로 치면 manifest파일이나 build-gradle 파일 같은 느낌 같다. 플러그인들을 관리한다.
+ drafts : 임시 보관함, 날짜 형식 x , title.markup으로 사용
+ includes : 말 그대로 레이아웃과 게시물들이 포함되서 재사용하게 한다. {% include file.ext %}를 사용해서 부분 포함시키다.
+ layouts : 게시물들의 레이아웃. {{content}}부분이 웹페이지 내용이다.
+ post : 여기에 내용들을 올린다. 이름 규칙이 쓸데없이 복잡하다.
+ data : 사이트의 데이터 저장소. `site.data`로 접근한다. members.yml은 `site.dat.members`로 접근한다.
