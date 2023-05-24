---
title: "Java Oracle 에러 로케일을 인식 할 수 없습니다 (M1)"
categories: java
tags: java mac m1 arm64
---

> Mac에서 메이저버전 OS 업데이트가 있으면 주로 발생한다.
> 아무래도 대규모 업데이트가 발생하면서 설정값이 초기화 되는 듯 하다.

## 1차 해결방법

* M1이 아닐때는 `언어 및 지역`에서 지역을 대한민국 -> 미국 -> 대한민국 으로 변경

## 2차 해결방법

* VM Option 추가

```shell
-Duser.language=ko -Duser.country=KR
```
