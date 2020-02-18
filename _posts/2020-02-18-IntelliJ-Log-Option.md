---
title: "IntelliJ IDEA Console Log Link"
categories: intellij
tags: intellij log
---

## 목표
> IntelliJ IDEA 출력시 로그 링크를 클릭하면 소스로 이동하게 한다.

## 환경
- Java 1.8
- IntelliJ IDEA 2019.3.3
- Spring Boot 2.2.4.RELEASE
- Logback

## 설정
[logback-extention](https://github.com/qos-ch/logback-extensions/wiki/Spring)을 사용하여 설정하기 보다는 `application.properties`를
이용한 설정이 편하다.

#### application.properties
```
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss.SSS} %magenta([%thread]) %highlight(%-5level) %msg - at %C.%M\\(%F:%L\\)%n
```
- `%d{yyyy-MM-dd HH:mm:ss.SSS}`:로그 날짜
- `%magenta([%thread])`: 로그 기록시 스레드
- `%highlight(%-5level)`:  로그 레벨
- `%msg`: 로그 메세지
- `%C.%M\\(%F:%L\\)%n`: <fully-qualified-class-name>.<method-name>(<file-name>:<line-number>) 형식으로 작성하면 된다. 
다만 application.properties 설정에서 소괄호 부분은 Escape 해줘야 한다.

## 참고
- [Setting Log Options](https://www.jetbrains.com/help/idea/setting-log-options.html)
- [Spring Custom Log Configuration](https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-custom-log-configuration)
- [Logback layouts](http://logback.qos.ch/manual/layouts.html)
