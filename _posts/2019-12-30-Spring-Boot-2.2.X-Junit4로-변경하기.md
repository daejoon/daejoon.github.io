---
title: "Spring Boot 2.2.X 에서 JUnit4로 변경하기"
categories: springboot
tags: java springboot junit
---

> Spring Boot 2.2.X 부터는 JUnit5가 기본이다. 아직은 익숙하지 않기때문에 JUnit4로 변경해서 사용한다.

## JUnit5 사용 
```
dependencies {
    ...
    testImplementation('org.springframework.boot:spring-boot-starter-test') {
        exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
    }
}

test {
	useJUnitPlatform()
}
```
- [start.spring.io](https://start.spring.io){:target="_blank"}로 생성하기

## JUnit4 사용
```
...
dependencies {
    ...
    testImplementation('org.springframework.boot:spring-boot-starter-test')
}

test {
    useJUnitPlatform {
        includeEngines 'junit-vintage'
        // excludeEngines 'junit-jupiter'
    }
}
...
```
- JUnit4 에서는 테스트 Class와 테스트 Method는 둘다 `Public` 이어야 한다.
