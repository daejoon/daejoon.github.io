---
title: "Parameter VS Argument"
categories: 혼동되는것  
tags: java
---

> 별개 다 혼동되어서 정리한다.

## 예제

```java
public class ParameterAndArgument {

    public void printHello(String message) {

        System.output.println("Hello " + message);
    }

    public static void main() {

        final String message = "world";
        new ParameterAndArgument().printHello(message);
    }

}
```

## Parameter (매개변수)

* 예제 에서 `message` 변수 이게 parameter 이다. 

## Argument (전달인자)

* 예제 에서 전달되는 `world` 값 이게 argument 이다.

## 참고

* [매개변수 (컴퓨터 프로그래밍)](https://ko.wikipedia.org/wiki/%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))