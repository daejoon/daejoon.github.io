---
title: "curl hosts 파일을 수정하지 않고 호출하기"
categories: linux
tags: shell linux mac
---

로컬에서 테스트를 위해서는 다양한 호출 방법이 있을수 있다.

* IP로 호출하기
* Domain으로 호출하기

경우에 따라서는 등록되어 있지 않지만 IP로 호출하면 안되는 경우도 있다 보통 서비스에서 도메인 형식을 체크해서 튕기도록 구성되어 있다.

이럴때 사용하면 좋은 방법이다.

보통은 /etc/hosts 파일을 수정하는데 수정하기도 귀찮고 테스트 끝나면 원복을 안하면 차후에 실수하기도 한다.

## 사용방법

```shell
curl --resolve '{도메인}:{포트}:{아이피}' {url}
```

### 사용예

```shell
curl --resolve 'blog.ddoong2.com:4000:127.0.0.1' http://blog.ddoong2.com:4000
```

* 로컬에서 Jekyll을 이용해서 띄울때 예제
* 우선 순위에 의해서 DNS 보다 먼저 설정 된다.