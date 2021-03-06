---
title: "IntelliJ IDEA SSH Tunneling으로 AWS RDS 접속"
categories: intellij
tags: intellij
---

## 목표
>IntelliJ IDEA에서 SSH Tunnel을 이용한 MariaDB 접속

## SSH Tunnel
### SSH 터널링
```
$ ssh -i <identity-file> -L -H <local-port>:<aws-rds-endpoint>:<aws-rds-port> ec2-user@<Bastion-Host>
```
- `<identity-file>`: AWS Instance를 접속하기 위한 키페어의 개인키
- `<local-port>`: 로컬 포트
- `<aws-rds-endpoint>`: AWS RDS 엔드포인트
- `<aws-rds-port>`: AWS RDS 포트
- `<Bastion-Host>`: AWS Bastion Instance 의 공개 IP

### MySQL Client 접속
```
$ mysql -h 127.0.0.1 -P <local-port> -u <aws-rds-user-id> -p <aws-rds-user-password>
```
- `<local-port>`: 터널링 할때 선언한 로컬 포트
- `<aws-rds-user-id>`: AWS RDS 접속 User
- `<aws-rds-user-password>`: AWS RDS 접속 password

## IntelliJ IDEA SSH Tunnel
IntelliJ IDEA Ultimate는 Database Plugin을 통해서 SSH Tunneling을 지원한다.

![](/assets/images/2019-12-15/IntelliJ-IDEA-SSH-Tunneling-01.png)
1. use SSH tunnel [선택]
2. Proxy Host: `<Bastion-Host>` 호스트 [입력]
3. Proxy port: SSH 접속 포트, 기본적으로 22번으로 고정된다.
4. Proxy user: Bastion 접속 User 인데 AWS는 대부분 ec2-user로 접속
5. Auth type: Key pair (OpenSSH or Putty) [선택]
6. Private key file: AWS 접속하기 위해 설정하게된 키페어의 개인키 여기서는 `<identity-file>`이 키페어 개인키이다.

![](/assets/images/2019-12-15/IntelliJ-IDEA-SSH-Tunneling-02.png)
1. Host: `<aws-rds-endpoint>` [입력]
2. Port: `<aws-rds-port>` 인데 여기서는 MariaDB를 사용해서 기본은 3306을 사용한다. 3306 [입력]
3. User: `<aws-rds-user-id>` [입력]
4. Password: `<aws-rds-user-password>` [입력]
5. 테스트 접속 확인: Test Connection 버튼 [선택]  
