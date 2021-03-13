---
title: "Macbook M1에서 빌드한 docker 이미지로 배포했을때 오류 발생"
categories: gitlab
tags: gitlab docker, m1
---

> 맥북에어 M1 에서 Gitlab Delopy용 컨테이너 이미지를 빌드후 배포 시도하니 오류 발생

## 오류 내용
```
standard_init_linux.go:190: exec user process caused "no such file or directory"
```

## 해결 방법
- 인텔용으로 재 빌드해서 배포

## 처리 방법
- gitlab용 docker 로그인  
```
$ docker login registry.gitlab.com -u {username} -p {password}
```
- 인텔용 이미지 빌드
```
$ docker buildx build --platform=linux/amd64 -t {image name}:{tag name} {Dockerfile path}
```
- 저장소 push
```
$ docker push {image name}:{tag name}
```
- 사실 인텔용 이미지로만 빌드하면 됨.
