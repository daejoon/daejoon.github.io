---
title: "Install Command Line Tool"
categories: mac
tags: mac
---

Command Line Tool을 설치하려면 기본적으로 Xcode를 설치해야 하지만 수동으로 설치 할 수도있다.

## Install Command Line Tool
```
$ sudo xcode-select --install
```

만약 설치할때 `xcode-select: error: command line tools are already installed, use "Software Update" to install updates`오류 메세지가 출력된다면 아래와 같이 해당 디렉토리를 삭제한후 다시 설치한다.
```
$ sudo rm -rf /Library/Developer/CommandLineTools
$ sudo xcode-select --install
```
