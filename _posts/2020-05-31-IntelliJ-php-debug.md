---
title: "IntelliJ IDEA에 PHP, Xdebug 설정"
categories: intellij
tags: intellij php
---

## 목표
> IntelliJ IDEA에 PHP 디버그 가능하게 설정 한다.

## 환경
- MacOS 10.15.5
- Homebrew
- PHP 7.4.6
- Xdebug 2.9.6
- IntelliJ IDEA Ultimate 2020.1
- Chrome

## 설정

### php 설치
```
$ brew install php
```

### xdebug 설치
```
$ pecl install xdebug
```

### 설치 정보 확인
```
$ php --version
PHP 7.4.6 (cli) (built: May 29 2020 01:44:57) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
    with Xdebug v2.9.6, Copyright (c) 2002-2020, by Derick Rethans
    with Zend OPcache v7.4.6, Copyright (c), by Zend Technologies
```

### php.ini 파일 수정
- `/usr/local/etc/php/7.4/php.ini` 아래 내용을 맨위에 추가
```
[xdebug]
zend_extension="/usr/local/lib/php/pecl/20190902/xdebug.so"
xdebug.remote_enable=1
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000
xdebug.remote_handler=dbgp
xdebug.profiler_enable=1
xdebug.profiler_output_dir=/tmp
```

### php 플러그인 설치
[![](/assets/images/intellij-php-01.png)](/assets/images/intellij-php-01.png)

### IntelliJ IDEA 설정
[![](/assets/images/intellij-php-02.png)](/assets/images/intellij-php-02.png)
[![](/assets/images/intellij-php-03.png)](/assets/images/intellij-php-03.png)
- Start Listening for PHP Debug connections 활성화
[![](/assets/images/intellij-php-05.png)](/assets/images/intellij-php-05.png)

### 크롬 Xdebug helper 설치
[![](/assets/images/intellij-php-04.png)](/assets/images/intellij-php-04.png)
- Debug 활성화
[![](/assets/images/intellij-php-06.png)](/assets/images/intellij-php-06.png)

## 참고
- [IntelliJ IDEA Configuration Xdebug](https://www.jetbrains.com/help/idea/2020.1/configuring-xdebug.html?utm_campaign=IU&utm_content=2020.1&utm_medium=link&utm_source=product#)
- [Browser debugging extensions](https://www.jetbrains.com/help/idea/2020.1/browser-debugging-extensions.html?utm_campaign=IU&utm_content=2020.1&utm_medium=link&utm_source=product)
- [Xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)
