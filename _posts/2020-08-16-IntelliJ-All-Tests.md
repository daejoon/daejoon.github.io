---
title: "IntelliJ IDEA에서 All Tests 실행시 폴더 접근 오류"
categories: intellij
tags: intellij java
---

## 증상
> IntelliJ IDEA에서 All Tests로 Unit 테스트 실행시키면 폴더 접근 오류 발생

## 해결
![](/assets/images/2020-08-16/2020-08-16-IntelliJ-All-Tests-01.png)
- All Tests를 작성 하고 실행한다.

![](/assets/images/2020-08-16/2020-08-16-IntelliJ-All-Tests-02.png)
- 폴더가 없다는 오류가 발생한다.

![](/assets/images/2020-08-16/2020-08-16-IntelliJ-All-Tests-03.png)
- 프로젝트 밑에 IntelliJ 가 관리하는 폴더가 있다. `.idea` 해당 폴더 밑에 `modules/{모듈명}` 의 폴더가 존재 해야 한다.
- 그래들 멀티 프로젝트로 만들었는데 직접 폴더를 생성하면서 문제가 발생한것 같다.
- 되도록이면 멀티 프로젝트를 만들때는 IntelliJ의 기능을 이용해서 루트 프로젝트를 만들고 그 다음에 모듈을 추가해서 하위 프로젝트를 만드는게 정신건강에 좋다.

## 느낀점
> 별것 아닌데 시간을 오래 잡아 먹었다. `./gradlew clean test` 하면은 잘 되는데 IntelliJ IDEA에서 실행하면 오류가 발생했다.
> 에러 메세지를 잘 확인하면 되는데 메세지는 스쳐지나가고 난 내 설정 문제가 있는줄 알고 착각하고 개발하면서 중요한 습관중 하나는 에러 메세지를
> 잘 확인하는 거라고 생각한다.