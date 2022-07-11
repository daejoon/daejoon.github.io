---
title: "Spring Boot None WebApplication Mode"
categories: springboot
tags: java springboot
---

> 열에 아홉은 스프링 부트 대부분 웹 어플리케이션 형식으로 사용하지만 간혹 CLI 형식의 명령어를 구동하기 위해서 만들고
> 싶을때가 있다.
> 아래와 같이 하면 된다. 너무 간단하다.

## application.yml

```
spring.main.web-application-type: none
```

* [Spring Boot WebApplication Type](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/WebApplicationType.html)

## Java 코드로는 아래와 같다.

```
@SpringBootApplication
public class WebApp {

    public static void main(String[] args) {
        final SpringApplication springApplication = new SpringApplication(WebApp.class);
        springApplication.setWebApplicationType(WebApplicationType.NONE);
        springApplication.run(args);
    }
}

```