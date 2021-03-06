---
title:  Mac Tunnerning To AWS Microsoft Remote Desktop
date:   2016-04-20 +0900
categories: aws
---

## 준 비 물
- SSH key: `{keyName}.pem`
- Terminal: 맥은 기본으로 탑재되어 있다.
- Microsoft Remote Desktop: `App Store`에서 다운로드 한다.

## 실행 방법
`{keyName}.pem` 파일이 있는 위치로 이동한다.
`{keyName}.pem` 파일의  권한을 변경한다. (권한은 한번만 변경하면 된다.)
```
$ chmod 400 {keyName}.pem
``` 
해당 명령어를 입력 한다. `ssh -i {keyName} {loginName@vpnDomainName} -N -L {localPort}:{remoteIp}:{remotePort}`
```
$ ssh -i sample.pem sample-user@vpn.sample.com -N -L 3389:10.10.10.10:3389
```
`-i`: 인증파일 사용
`-N`: 원격명령을 실행하지 않는다. (protocal version 2 only)
`-L`: `[bind_address:]port:host:hostport`

오류가 나지 않으면(아무반응이 없으면) 터널링이 연결된 것이다.
이상태에서 `Microsoft Remote Desktop`으로 접속하면 된다. (remoteIP로 접근 로그인과 패스워드를 입력)

## 참고
- [Aws SSH 사용](http://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
- [Azure SSH 사용](https://azure.microsoft.com/ko-kr/documentation/articles/virtual-machines-linux-ssh-from-linux/)
- [SSH 터널링 옵션](https://blog.lael.be/post/845)
