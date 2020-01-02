---
title: "Querydsl build.gradle 설정"
categories: gradle
tags: gradle java springboot
---

구글링을 해보면 Gradle을 이용해서 QueryDsl 설정 방법은 대체로 두가지로 나온다.

첫번째는 [`com.ewerk.gradle.plugins.querydsl`](https://plugins.gradle.org/plugin/com.ewerk.gradle.plugins.querydsl){:target="_blank"} 플러그인을 이용하는 방법이고 두번째는 `build.gradle`안에 스크립트를 작성하는 방법이다.

첫번째 방법은 실행하면 `IntelliJ IDEA`에서 `Build and run using` 설정을 `IntelliJ IDEA`로 설정시 QClass 파일을 찾지 못하는 오류가 발생한다.
`Gradle (Default)`을 설정하면 Gradle로 빌드하면 되는데 `IntelliJ IDEA`의 `Rebuild Project`를 하면 역시 QClass 파일을 찾이 못하는 오류가 발생한다.
하여 두번째 빌드 스크립트를 이용하는 방법을 선택했다.

## 실행 환경
- IntelliJ IDEA 2019.3.1
- Gradle 4.10.2
- Java 1.8

## build.gradle
```
...

/** QueryDSL Class Generate Script */
def generatedJavaSrcDir = 'src/main/generated'
def queryDslOutput = file(generatedJavaSrcDir)

sourceSets {
    main {
        java {
            srcDirs = ['src/main/java', generatedJavaSrcDir]
        }
    }
}

/** QClass 생성 */
task generateQueryDSL(type: JavaCompile, group: 'build') {
    doFirst {
        delete queryDslOutput
        queryDslOutput.mkdirs()
    }
    source = sourceSets.main.java
    classpath = configurations.compile
    destinationDir = queryDslOutput
    options.compilerArgs = [
            '-proc:only',
            '-processor',
            'com.querydsl.apt.jpa.JPAAnnotationProcessor'
    ]
}
compileJava.dependsOn(generateQueryDSL)

/** clean 태스크 실행시 QClass 삭제 */
clean {
    delete queryDslOutput
}
```
