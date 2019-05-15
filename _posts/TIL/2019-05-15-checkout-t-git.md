---
layout: post
title: create and pull remote branch to local at once
categories: TIL
---
To pull the remotes branch, I used to 
```
git checkout [-b] NEW_BRANCH_NAME
git pull origin REMOTE_BRANCH_NAME
```
but recently what I am doing is
```
git checkout -t origin FULL_REMOTE_BRANCH_NAME
// git checkout -t origin remotes/origin/BRANCH_NAME
```
Then branch with the same branch name will be created.
