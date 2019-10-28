---
layout: post
title: create and delete remote branch to local at once(modified)
categories: TIL
---

## create and pull remote branch to local at once
To pull the remotes branch, I used to 
```
git checkout [-b] NEW_BRANCH_NAME
git pull origin REMOTE_BRANCH_NAME
```
but recently what I am doing is
```
git branch -t origin FULL_REMOTE_BRANCH_NAME
// git branch -t origin remotes/origin/BRANCH_NAME
```
Then branch with the same branch name will be created.

## remove remote branch from local
To remote the remote branch from local this would work.
```
git push origin --delete BRANCH_NAME
```
