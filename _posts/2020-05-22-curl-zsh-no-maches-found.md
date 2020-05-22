---
title: "zsh: no matches found:"
categories: zsh
tags: zsh
---

## 목표
> zsh(ohmyzsh) 쉘에서 curl 사용이 `zsh: no matches found`가 발생한다.


## .zshrc 수정
```
alias curl='noglob curl'
```

## 참고
[zsh: no matches found](https://github.com/ohmyzsh/ohmyzsh/issues/31)
