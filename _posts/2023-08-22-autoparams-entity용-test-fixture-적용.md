---
title: "AutoParams에서 Entity를 Test Fixture로 사용할때 컬럼제한 해결 하기"
categories: java
tags: java autoparams test entity fixture
---

## 배경

[`AutoParams`](https://github.com/AutoParams/AutoParams)을 참 요긴하게 사용하고 있다. 웬만한 파라미터는 기본적으로 지원하는데
`@Entity`의 경우는 데이터베이스 컬럼에 영향을 받아서 AutoParams으로 만들어진 데이터를 가지고 테스트 하다보면 디비 컬럼 Length 조건에 
걸려서 오류가 나는 경우가 발생한다. 이런 경우는 [`Customizer`](https://github.com/AutoParams/AutoParams#customization-annotation) 확장 포인트를 열어뒀다. 그걸 이용해서 `@Column`의 Length를 읽어서 
값을 제한하게 하였다. 아래는 구현코드 이다.

## 코드

<script src="https://gist.github.com/daejoon/e32c83ac6427e234354b79bb8f000c74.js"></script>

<script src="https://gist.github.com/daejoon/a17e7acbfd121749a66e5a823c11be34.js"></script>

## 사용법

```java
@ParameterizedTest
@AutoSource
@Customization(DomainCustomization.class)
void test(MyEntity entity) {
    ...
}
```