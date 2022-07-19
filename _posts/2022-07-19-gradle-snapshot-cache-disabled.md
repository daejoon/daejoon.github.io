---
title: "Gradle SNAPSHOT Dependency 캐쉬 Disabled 하기"
categories: java  
tags: java gradle
---

> 버저닝을 로드맵에 따라 계획적으로 잘하면 되지만 현실에서는 계획적인 버저닝을 하기는 쉽지 않다. 그래서 내부적으로 사용하고 
> 변경이 잦으면 SNAPSHOT으로 사용하기도 한다. 그런데 SNAPSHOT도 캐쉬가 되어서 변경사항이 잘 반영이 안되는데 그럴때는
> Cache를 Disabled 처리해야 한다.


## build.gradle

### repositories 수정

* dependency 가 SNAPSHOT일때는 스냅샵용 레파지토리를 추가한다. 아래는 spring의 snapshot maven을 추가한 예제이다.

```groovy
...
repositories {
    mavenCentral()
    if (version.endsWith('-SNAPSHOT')) {
        maven { url "https://repo.spring.io/snapshot" }
    }
}
...
```

### configuration 추가

* SNAPSHOT도 캐쉬타임이 있는데 기본으로 24시간이다. 0으로 변경

```groovy
...    
configurations.all {
    resolutionStrategy.cacheChangingModulesFor 0, "minutes"
}
...
```

### dependencies 수정

* 아래와 같이 Changing = true로 cache disabled 기본은 false 이다.

```groovy
...
denpendencies {
    implementation("{groupId}:{artifactId}:{version}-SNAPSHOT") {
        changing = true
    }
}
...
```

## 참고

* [Handling versions which change over time](https://docs.gradle.org/7.4.2/userguide/dynamic_versions.html)
* [Interface ExternalModuleDependency](https://docs.gradle.org/7.4.2/javadoc/org/gradle/api/artifacts/ExternalModuleDependency.html#setChanging-boolean-)

