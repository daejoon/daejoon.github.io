---
title: "OpenVPN on Docker"
categories: docker
tags: aws openvpn docker
---

## 도커 설치 및 환경 구성
### 패키지 캐쉬 업데이트
```
$ sudo yum update -y
```

### 도커 설치
```
$ sudo yum install docker
```

### 도커 서비스 시작
```
$ sudo service docker start
```

### docker 그룹에 sudo를 추가
```
$ sudo usermod -a -G docker ec2-user
```

### 다시 로그인

### 도커 명령 확인
```
$ docker info
```
- 경우에 따라서는 재부팅 해야 하는 경우도 있다.

## OpenVPN 설치 및 환경 구성
### OpenVPN 설정 파일을 저장할 데이터 디렉토리를 환경변수 등록
```
$ OVPN_DATA="/home/ec2-user/openvpn-data"
```

### docker 이미지 생성 및 초기화
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://<hostname>
```
- `<hostname>`은 실제 도메인으로 지정

### OpenVPN의 CA Certificate와 Server key 생성
```
sudo docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn ovpn_initpki
```

### CA 키 생성
```
...
Enter pass phrase for /etc/openvpn/pki/private/ca.key: <ca-password>
Re-Enter New CA Key Passphrase: <ca-password>
...
Common Name (eg: your user, host, or server name) [Easy-RSA CA]: <common-name>
```
- `<ca-password>`를 이용해서 유저를 생성한다
- `<common-name>`은 Default 선택: 엔터 입력하면 된다.
키 생성이 계속 무한대로 진행하는 경우가 있는데 그럴때는 `/home/ec2-user/openvpn-data`를 삭제하고 다시 진행한다.

### Open VPN 서버 실행
```
$ docker run -v $OVPN_DATA:/etc/openvpn -d -p 1194:1194/udp --restart=always --cap-add=NET_ADMIN kylemanna/openvpn
```
- `--restart=always`:  커맨드를 실행시켜서 혹시나 docker 컨테이너가 실행이 중단되는 경우에도 곧바로 다시 restart가 되도록 설정
- `--cap-add=NET_ADMIN`: Linux의 추가 기능을 사용 ([CAP_NET_ADMIN](https://linux.die.net/man/7/capabilities))

## OpenVPN 클라이언트 설정
### 클라이언트 유저 생성
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full <client-user-name> nopass
```
- `<client-user-name>`: 클라이언트 접속 유저 이름
- `nopass`를 제거하면 아이디, 비밀번호 입력 방식으로 변경된다.

### 클라이언트 설정 파일 호스트(docker container to host)로 복사
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient <client-user-name> > <client-user-name>.ovpn
```

### 클라이언트 제거
```
$ docker run --rm openvpn ovpn_revokeclient <client-user-name> remove
```
- 클라이언트 관련 문제가 발생하거나 기존 계정 삭제시 사용

## VPN을 통한 인터넷 접속및 Private 네트워크 접속
### vi로 컨테이너의 /etc/openvpn/openvpn.conf 파일 오픈
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn vi /etc/openvpn/openvpn.conf
```

### 환경 설정 수정
```
...
### Route Configurations Below
route 192.168.254.0 255.255.255.0

### Push Configurations Below
#push "block-outside-dns"
#push "dhcp-option DNS 8.8.8.8"
#push "dhcp-option DNS 8.8.4.4"
push "comp-lzo no"
push "route <vpc-ip> <vpc-netmask>"
```
- `push "route <vpc-ip> <vpc-netmask>"`: 이부분을 추가해야지 인터넷 가능
- 예) `push "10.10.0.0 255.255.0.0"`

## 참고
- [Amazon ECS의 도커 기본 사항](https://docs.aws.amazon.com/ko_kr/AmazonECS/latest/developerguide/docker-basics.html)
- [Dockerhub kylemanna/openvpn](https://hub.docker.com/r/kylemanna/openvpn/)
- [Github docker-openvpn](https://github.com/kylemanna/docker-openvpn)
- [Docker로 OpenVPN 쉽게 설치하기](https://rampart81.github.io/post/openvpn_aws/)
- [원격근무의 필수조건, AWS에 OpenVPN 구축기](https://elegantcoder.com/aws-openvpn-begins/)
