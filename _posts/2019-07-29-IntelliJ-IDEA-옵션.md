---
title: "IntelliJ IDEA VM Options..."
categories: intellij
tags: mac
---

IntelliJ IDEA 버전업을 할때마다 점점 느려지더니 2019.1에 와서는 3기가 메모리까지 올리는 상황이 발생했다.

개인적으로 성능측정을 진짜 무식하게 하는 편인데

1. 내가 가지고 있는 나름 해비한 프로젝트를 오픈한다.
2. `File` -> `Invalidate Caches / Restart...` -> `Invalidate and Restart` 누른다.
3. 프로젝트 다시 로딩하고 몇개의 파일을 열어서 파일간의 전환이 버벅이는지 확인한다.

2019.1.X 버전에서는 2기가의 Heap 메모리가 버티지 못해서 메모리 적다고 오류 발생했었다. 그래서 3기가로 올렸었다.
이번에 2019.2 버전에서는 정말 쾌적하다 그래서 3기가에서 2기가로 힙 메모리를 다시 낮췄다.

## Custom VM options

- 위치: `Help -> Edit Custom VM Options...`

아래는 내가 사용하는 옵션이다.

```
-Xms2g
-Xmx2g
-XX:ReservedCodeCacheSize=256m
-XX:+UseG1GC
-XX:MetaspaceSize=768m
-XX:MaxMetaspaceSize=768m
-XX:+UseCompressedOops
-XX:MaxGCPauseMillis=200
-XX:ParallelGCThreads=4
-XX:ConcGCThreads=1
-XX:+HeapDumpOnOutOfMemoryError
-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof
-ea
-server
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-Dfile.encoding=UTF-8
```

- `Xms`: 초기 Heap 사이즈
- `Xmx`: 최대 Heap 사이즈
- `XX:ReservedCodeCacheSize`: 코드 캐쉬 사이즈 Heap 메모리 사이즈와 공유하지 않는다.
- `XX:+UseG1GC`: G1GC 가비지 컬랙션을 사용한다.
- `XX:MetaspaceSize`: Java8 이상의 Permanent 영역 사이즈
- `XX:MaxMetaspaceSize`: Java8 이상의 최대 Permanent 영역 사이즈
- `XX:+UseCompressedOops`: 64비트 JVM에서 압축 참조를 사용 가능
- `XX:MaxGCPauseMillis`: GC로 인한 최대 중단시간을 명시
- `XX:ParallelGCThreads`: 다중 GC를 위해 사용되어질 GC 스레드의 수
- `XX:ConcGCThreads`: 동시적 CMS 단계가 동작할때에 사용할 쓰레드 개수를 정의
- `XX:+HeapDumpOnOutOfMemoryError`: OutOfMemoryError 발생 시 자동으로 heap dump를 생성
- `XX:ErrorFile`: 에러파일 생성 위치
- `XX:HeapDumpPath`: HeapDump 파일 생성 위치
- `ea`: assertions을 사용한다.
- `server`: 자바 HotSpot Server VM
- `Dsun.io.useCanonCaches`: Java의 정규화 캐시 사용여부
- `Djava.net.preferIPv4Stack`: IP4를 사용여부
- `Dfile.encoding`: Java 소스파일 인코딩

## 2023-02-04 기준 아래와 같이 사용한다

```
# Custom IntelliJ IDEA VM Options

-Xms2048m
-Xmx4096m

-XX:+UseG1GC
-XX:NewRatio=1
-XX:MaxGCPauseMillis=50
-XX:GCTimeRatio=19
-XX:ParallelGCThreads=8
-XX:ConcGCThreads=2

-Djava.net.preferIPv4Stack=true
```

## 참고

- [IntelliJ Configure JVM Options](https://www.jetbrains.com/help/idea/tuning-the-ide.html#configure-jvm-options)
- [VM Option](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html)
- [유용한 JVM 플래그들](http://linux.systemv.pe.kr/%EC%9C%A0%EC%9A%A9%ED%95%9C-jvm-%ED%94%8C%EB%9E%98%EA%B7%B8%EB%93%A4-part-4-%ED%9E%99-%ED%8A%9C%EB%8B%9D/) 


