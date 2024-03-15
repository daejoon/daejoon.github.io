---
title: "Git 확장 함수를 만들어 보자"
categories: shell
tags: git shell
---

# Git 확장함수

git을 사용하다 보면은 명령어가 길어져서 거추장 스러울때가 있다. 
난 개인적으로 특히 브랜치를 업데이트 할때 그 브랜치로 checkout을 한후 업데이트를 해야 하는데
업데이트 하려는 브랜치가 많다 보면은 이게 정말 일이다. 
그렇다고 GUI 툴을 사용하는것도 아니어서 브랜치 관련해서 업데이트 할려면 정말 귀찮아서 어떻게 하면
줄일수 있을까 고민하다가 Shell function 만드는 것으로 해결 봤다.

## 사용 방법

* `.zshrc` 에 코드를 넣는다.
<script src="https://gist.github.com/daejoon/a05347f454ee63a13049c7b36c1b735a.js"></script>

* 현재 브랜치를 최신화 한다. 브랜치 명을 선언하지 않으면 현재 브랜치 업데이트
```shell
git-update
```
* 현재 브랜치를 checkout 하지 않고 다른 브랜치를 업데이트 하는 방법
```shell
git-update develop
```
