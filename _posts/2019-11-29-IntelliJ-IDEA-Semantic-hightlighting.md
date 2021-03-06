---
title: "IntelliJ IDEA Semantic Highlighting"
categories: intellij
tags: intellij
---

IntelliJ IDEA(이하 IJ)를 사용하다 보면은 참 소소한 기능이 많다는 것을 느낀다. 평소 코드를 보면 변수와 파라미터명이
회색으로 잘 구별이 되지 않는데 아래 옵션을 활성화 하면은 색상별로 하이라이팅이 되어서 보기 편하다.

## Semantic Highlighting
![](/assets/images/2019-11-29/IntelliJ-Semantic-highlighting.png)
- `Preferences`->`Editor`->`Color Scheme`->`Language Defaults`->`Semantic highlighting`->[선택]

## Identifiers
![](/assets/images/2019-11-29/IntelliJ-Semantic-highlighting%202.png)
- `Preferences`->`Editor`->`Color Scheme`->`Language Defaults`->`Identifiers`->[선택]
- Local variable, Parameter, Reassigned local variable, Reassigned parameter 항목의 `Foreground`를 원하는 색상으로 변경하면 파라미터와 변수의 색상이 변경된다. 단 이 기능은 `Semantic Highlighting` 기능이 켜져있으면 적용되지 않는다.
