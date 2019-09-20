---
title: find for mac
date: 2016-12-19 11:00:00 +0900
categories: mac
---

windows에서는 파일 안의 특정 문자열을 검색해조 찾을수 있는 `findstr`란 명령어가 있다.

유닉스 계열에서는 `find` + `grep` 명령어로 대체할수 있다.

```
$ find ./ -name "<검색 파일명>" -print | xargs grep -n "<검색 문자열>" > <결과를 저장할 파일>
```

- 검색 파일명: `*`등 와일드 카드가 먹는다.
- 검색 문자열: 정규표현식을 사용할수 있다. `-E` 옵션
