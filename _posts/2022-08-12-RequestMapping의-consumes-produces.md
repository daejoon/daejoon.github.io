---
title: "RequestMapping의 Consumes와 Produces"
categories: 혼동되는것  
tags: spring java
---

> 사용할때마다 너무 헷갈린다. 그래서 정리해봤다.

## consumes

* @RequestMapping 류에서 사용되며 요청을 제한한다.
* 클라이언트가 요청시 Content-Type 헤더를 통해서 서버에 전달한다.
* `Content-Type=application/json`이면 클라이언트가 서버에 요청할때 내가 보내는 요청 정보는 `application/json`입니다. 라는 의미이다.

## produces

* @RequestMapping 류에서 사용되며 응답을 제한한다.
* 클라이언트가 요청시 Accept 헤더를 통해서 서버에 전달한다.
* `Accept=application/json`이면 서버가 응답하는 형식은 `application/json` 형식을 기대한다는 것이다.

## 개인적 추천

* 모든 요청과 응답에 대해서 정확하게 지정하는게 맞겠으나 개인적으로 consumes은 지정하는 편이고 produces는 지정하지 않는 편이다.

## 참고

* [@RequestMapping의 produces,Content-Type,Consumes란?](https://2ham-s.tistory.com/292)