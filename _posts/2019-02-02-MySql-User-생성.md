---
title: MySQL 유저 생성
categories: MySQL
---

> 개발하면서 테스트 용도로 사용하는데 매번 잊어버려서 정리 한다.
> 개발하면서 편의성 위주로 정리하기 때문에 실무에서는 외부 접근 및 권한에 신경을 써야한다.

## 콘솔 접속
```
$ mysql -uroot -p
```

## 디비 생성 및 확인
```
$ create databaes <디비이름>;
$ show databases;
```

## 유저 생성
```
$ create user '<사용자>'@'%' identified by '비밀번호';
```
- `%`:모든 접근 가능, `localhost`로 변경하면 로컬만 접속할수 있다. IP를 넣는다면 특정 IP만 제한할수 있다.

## 권한 부여
```
$ grant all privileges on <디비이름>.* '<사용자>'@'%';
```

## 디비 삭제
```
$ drop database <디비이름>;
```

## 유저 삭제
```
$ drop user '<사용자>'@'%';
```
