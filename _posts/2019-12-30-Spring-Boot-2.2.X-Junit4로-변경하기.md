---
title: "Spring Boot 2.2.X 에서 Junit4로 변경하기"
categories: springboot
tags: java springboot junit
---

> Spring Boot 2.2.X 부터는 Junit5가 기본이다. 아직은 익숙하지 않기때문에 Junit4로 변경해서 사용한다.

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
