---
title: "Mac에서 Android Device Monitor Freezing 현상"
date: 2018-03-09 00:21:00 +0900
categories: mac
tags: android
---

맥에서 `IntelliJ IDEA`를 이용해서 안드로이드 프로그램을 개발하는데 어느 순간부터 `Android Device Monitor`의 프리징 현상이 나타났다. 이것 저것 별짓을 해봐도 안됐었는데 [Stackoverflow](https://stackoverflow.com/questions/47089757/android-device-monitor-freezes-on-mac-os-x)의 이것이 힌트가 되어서 해결하게 되었다.

원인은 JDK 특정 버전에서 프리징 현상이 나타나서 구버전(jdk-8u151)으로 롤백해서 해결했다는 것이다. 구버전 JDK는 오라클 홈페이지 가서 아카이브된 파일을 찾아서 인스톨 해서 해결했다. 처음에는 `homebrew`를 이용해서 설치하려고 했는데 문제가 발생해서 못했다. 

왜냐고 하면 이야기가 길어지는데(이건 다음 포스트에서 다룰 예정) 간략히 이야기 하자면 JDK를 `homebrew`를 이용해서 관리하는 중이라 특정버전 설치가 나름 까다롭다. 예전에는 명령어가 있었는데 현재는 Deprecate되어서 사용할수 없었고 결국 하는 방법을 찾았지만 오라클 `Java8 jdk-8u151` 버전의 링크가 변경되어서 404로 파일을 찾을수 없었다. 결국 Java는 수동으로 설치했다.
