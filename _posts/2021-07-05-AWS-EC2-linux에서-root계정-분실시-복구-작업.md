---
title: "AWS EC2 linux에서 root 계정 분실시 복구 작업"
categories: aws
tags: aws linux ec2 linux
---

## 참고
[AWS EC2 linux 에서 root계정 비밀번호 분실 시 어떻게 해야하나요?](https://support.xavis.kr/hc/ko/articles/360022034731-AWS-EC2-linux-%EC%97%90%EC%84%9C-root%EA%B3%84%EC%A0%95-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8-%EB%B6%84%EC%8B%A4-%EC%8B%9C-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%B4%EC%95%BC%ED%95%98%EB%82%98%EC%9A%94-)

> 링크보다 잘 작성할 자신 없어서 옮겼습니다.

1. 임시 EC2 instance 생성 (분실한 EC2 instance와 동일한 OS)
2. 분실한 EC2 instance 서버 stop
3. 분실한 EC2 instance의 루트 volume Detach
4. 분실한 EC2 instance의 루트 volume 을 임시의 EC2 instance에 Attach (/dev/xvdb)
5. 임시 EC2 instance로 ssh 접속
6. ec2-user에 root 권한 부여
```
sudo -i
```
7. 임시 폴더 생성
```
mkdir /tempmnt
```
8. 분실한 EC2 instance의 root volume 마운트
```
mount /dev/xvdb /tempmnt
```
9. chroot를 사용하여 root 볼륨 변경
```
chroot /tempmnt
```
10. root 패스워드 변경
```
passwd root
```
11. exit명령어로 원래 root로 변경
```
exit
```
12. /tempmnt 마운트 해제
```
umount /tempmnt
```
13. 분실한 EC2 instance의 root 볼륨을 다시 원래대로 Dettach , Attach 작업 하여 복구
14. 임시 EC2 instance 삭제

## 주의사항
- root 볼륨의 Detach 작업은 EC2 instance가 stop 상태에서만 가능합니다.
- EBS의 Detach 작업은 반드시 마운트 해제를 해주셔야 완료됩니다.
