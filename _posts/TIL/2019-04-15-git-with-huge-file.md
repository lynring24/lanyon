---
layout: post
title:  Removing sensitive files from .git/server
categories: GIT
---

이전 버전에서는 문제가 없었던 파일이 깃허브 저장소의 크기를 초과해서 푸쉬를 할 수 없었다. 아쉽게도 해당 파일은 여러 브랜치에 들어 있었고, 꽤 오랫동안 git에서 관리해왔기 때문에 단순히 git에서 remove한다고 문제가 해결되지 않았다. 

[Removing sensitive file][https://help.github.com/en/articles/removing-sensitive-data-from-a-repository] 문서를 참고했다. 아래 명려어를 사용하면 파일을 삭제할 수 있다.

> git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch FILE_NAME_HERE' --prune-empty --tag-name-filter cat -- --all
