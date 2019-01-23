---
title: "IntelliJ IDEA에서 안드로이드 개발시 Layout Preview 한글깨짐"
date: 2018-01-03 11:49:00 +0900
categories: mac
---

[여기](http://thdev.tech/androiddev/2016/09/21/Android-Studio-Layout-Preview-Not-Korean.html)를 참고했다.

위에 예제는 `Android Studio 2.2`을 기준으로 설명했다.

난 `IntelliJ IDEA 2017.3.2`에서 적용했다.

해당 설정은 IntelliJ가 업그레이드 될때마다 한글이 깨진다. 

폰트가 없어져서 그런듯 

`fonts.xml`은 한번 설정 하면 되지만 폰트는 업그레이드 시마다 받아야 한다.

## 폰트 다운로드
```
$ curl https://gist.githubusercontent.com/skyisle/4d98cbcdc259601fba0f07602667b1b9/raw/0da59a462366f2d5165e112648a549cb705e9e15/korean_font.diff | patch -p1 -d /Applications/IntelliJ\ IDEA.app/Contents/plugins/android/lib/layoutlib/data/fonts/
```
나에게 맞게 경로를 수정했다.

## fonts.xml 수정
```
<family lang="ko">
  <font weight="400" style="normal" index="1">NanumGothic.ttf</font>
</family>
```
사용할 폰트 추가
