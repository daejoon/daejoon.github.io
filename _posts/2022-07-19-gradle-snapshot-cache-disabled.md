---
title: "Gradle SNAPSHOT Dependency 캐쉬 Disabled 하기"
categories: java  
tags: java gradle
---

## build.gradle

### repositories 수정

* denpencies가 SNAPSHOT일때는 스냅샵용 레파지토리를 추가한다.

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
    implementation("{groupId}.{artifactId}:{version}-SNAPSHOT") {
        changing = true
    }
}
...
```

## 참고

* [Handling versions which change over time](https://docs.gradle.org/7.4.2/userguide/dynamic_versions.html)
* [Interface ExternalModuleDependency](https://docs.gradle.org/7.4.2/javadoc/org/gradle/api/artifacts/ExternalModuleDependency.html#setChanging-boolean-)

