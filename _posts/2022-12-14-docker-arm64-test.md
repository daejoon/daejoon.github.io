---
title: "Docker arm64로 테스트 할때 Architecture간 오류 해결"
categories: mac  
tags: mac m1 arm64
---

> 대부분의 예제는 x86을 대상으로 이미지가 생성되어 있다. 특히 동영상 강좌나 예제를 실행할때 Architecture 간 오류가 발생하면
> 직접 arm64용으로 이미지를 만들어야 한다.

## 해결방법

* M1에서 빌드 한다.
* 이미지 빌드

```shell
$ docker build . {account_id}/{image_name}:{tag_name}
```

* Docker Hub 로그인

```shell
$ docker login
```

* 이미지 Push

```shell
$ docker push {account_id}/{image_name}:{tag_name}
```

* 사용 예
    * tag 버전을 붙이지 않으면 Latest로 가져온다.

```shell
$ docker run -d {account_id}/{image_name}:{tag_name}
```

## 참고

* [Install Docker Buildx](https://docs.docker.com/build/install-buildx/)를 이용하면 Multi-Architecture
  빌드가 가능하다
* [github docker/buildx](https://github.com/docker/buildx#windows-and-macos)
* 맥설치

```shell
$ brew install docker-buildx
```

* 실행권한 추가

```shell
$ chmod +x ~/.docker/cli-plugins/docker-buildx
```

* Multi build

```
$ docker buildx build --platform linux/amd64,linux/arm64 . {account_id}/{image_name}:{tag_name}
```