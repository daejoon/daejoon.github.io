---
title: "Git .gitconfig의 alias 설정"
categories: git
tags: git
---

## 목표
> 자주 사용하는 설정중 alias 부분을 기록한다.

## Alias
```
[alias]
    lg = log --graph --full-history --all --color --pretty=format:'%Cred%h%x09%Creset %C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
    st = status
    ss = status -s
    fa = fetch --all
    br = branch
    co = checkout
    pr = "!f() { git fetch -fu ${2:-origin} refs/pull/$1/head:pr/$1 && git checkout pr/$1; }; f"
    pr-clean = "!git for-each-ref refs/heads/pr/* --format='%(refname)' | while read ref ; do branch=${ref#refs/heads/} ; git branch -D $branch ; done"
    df = "diff"
    ld = "log -p -1"
```
