---
title:  Spring Boot에서 Undertow 사용하기
categories: springboot
tags: java spring
---

>[Undertow](http://undertow.io/)는 NIO를 기반으로 하는 고성능 웹서버이다. 전반적으로 성능이 우수하고 메모리 사용이 효율적이다. 
>[참고(Spring Boot Servlet Container)](https://www.baeldung.com/spring-boot-servlet-containers)

## 환경
- 스프링부트 버전은 `Spring Boot 2.1.2.RELEASE` 
- 빌드 툴은 `gradle`
- Spring Boot의 설정 파일을 `.yml`을 사용

## 설정 방법
- build.gradle에 `dependencies`를 추가한다. `spring-boot-starter-web`은 내장 톰켓을 사용하고 있다. 내장 톰켓을 `exclude` 시키고 `spring-boot-starter-undertow`를 추가한다.
    ```gradle
    dependencies {
        ...
        compile("org.springframework.boot:spring-boot-starter-web") {
            exclude group: "org.springframework.boot", module: "spring-boot-starter-tomcat"
        }
        compile ("org.springframework.boot:spring-boot-starter-undertow")
        ...
    }
    ```
- Web Application Server의 접속 정보를 기록하고 싶으면 환경 설정 파일에 `server.undertow` 부분을 추가한다. 설정방법은 [Appendix A. Common application properties](https://docs.spring.io/spring-boot/docs/2.1.2.RELEASE/reference/htmlsingle/#common-application-properties)를 참고한다. accesslog.pattern 부분은 [Configure Access Logging](https://docs.spring.io/spring-boot/docs/2.1.2.RELEASE/reference/htmlsingle/#howto-configure-accesslogs)을 참고한다.
    ```yaml
    ...
    server.undertow.accesslog.dir: # Undertow access log directory.
    server.undertow.accesslog.enabled: true # Whether to enable the access log.
    server.undertow.accesslog.pattern: %t %a "%r" %s (%D ms) # Format pattern for access logs.
    server.undertow.accesslog.prefix: access_log. # Log file name prefix.
    server.undertow.accesslog.suffix: log # Log file name suffix.
    ...
    ```
    문서를 보면 톰켓 설정과 다르게 특이하게 prefix 부분에 `accessP_log.`로 마지막에 점(.)이 들어가 있고 `suffix`는 시작 부분에 점(.)이 빠져있다.

## 마치며
스프링 부트의 디펜던시를 변경하는 것 만으로도 Tomcat에서 Undertow으로 `Embedded Servlet Container`을 변경할수 있다. 다시 한번 Spring Boot의 편리함을 느낄수 있다.
