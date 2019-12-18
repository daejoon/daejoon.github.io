---
title: "OpenVPN Two-factor"
categories: docker
tags: aws openvpn docker
---

## 목표
Google-Authenticator를 이용해서 로그인한다.

[OpenVPN on Docker](/2019/12/18/OpenVPN-On-Docker/)

## 설치 방법
### OpenVPN 환경설정
```
# OVPN_DATA=/home/ec2-user/openvpn-data
# CIPHER=AES-256-CBC
$ docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_genconfig -u udp://<hostname> -2 -C $CIPHER
```
- `<hostname>`: 실제 사용하는 호스트 네임
- [Cipher 종류](https://openvpn.net/vpn-server-resources/how-to-change-the-cipher-in-openvpn-access-server/)

### vi로 컨테이너의 /etc/openvpn/openvpn.conf 파일 오픈
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn vi /etc/openvpn/openvpn.conf
```

### 환경 설정 수정
```
...
### Push Configurations Below
#push "block-outside-dns"
#push "dhcp-option DNS 8.8.8.8"
#push "dhcp-option DNS 8.8.4.4"
push "comp-lzo no"
push "route <vpc-ip> <vpc-netmask>"
```
- `push "route <vpc-ip> <vpc-netmask>"`: 이부분을 추가해야지 이터넷 가능

### 클라이언트 유저 생성
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm -it kylemanna/openvpn easyrsa build-client-full <client-user-name> nopass
```
- `<client-user-name>`:  클라이언트 접속 ID

### 클라이언트 QR 코드 생성
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm -i kylemanna/openvpn ovpn_otp_user <client-user-name>
```

### Google Authenticator 인식
[![](/assets/images/2019-12-19-OpenVPN-On-Docker-Two-factor-01.png)](/assets/images/2019-12-19-OpenVPN-On-Docker-Two-factor-01.png)
1. QR코드 링크 Url로 들어가면 이미지가 보인다. Google Authenticator의 바코드 스캔을 한다.
2. `Enter code From app (-1 to skip): ` 이부분에 인식된 OTP 코드 6자를 넣는다.
3. `QR코드 링크`, `Emergency scratch codes`는 백업 해둔다.

### 클라이언트 설정 파일 호스트(docker container to host)로 복사
```
$ docker run -v $OVPN_DATA:/etc/openvpn --rm kylemanna/openvpn ovpn_getclient <client-user-name> > <client-user-name>.ovpn
```

### Tunnelblick 접속
[![](/assets/images/2019-12-19-OpenVPN-On-Docker-Two-factor-02.png)](/assets/images/2019-12-19-OpenVPN-On-Docker-Two-factor-02.png)
1. `<client-user-name>` 명 입력
2. Google Authenticator의 숫자 6개 입력


## 참고
[docker-openvpn OTP](https://github.com/kylemanna/docker-openvpn/blob/master/docs/otp.md)
