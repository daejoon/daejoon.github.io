---
title: Charles Proxy 설정
date: 2018-03-04 11:24:33 +0900
categories: mac
---

> Charles 최신버전으로 Proxy를 처리하는 글이 없어서 찾으면서 삽질한 내용을 정리 했다.
> iOS나, Android도 비슷하다.

## SSL Proxying Settings...

* `Proxy | SSL Proxying Settings...` [선택]
* `SSL Proxying | Enable SSL Proxying` [선택]
  ![](/assets/images/2018-03-04/ssl-proxying.png)
* `ADD` [선택]
* `Host` * [입력]
* `Port` 443, 8443 [입력]
* `Ok` [선택]

## Install Charles Root Certificate

* `Help | SSL Proxying | Install Charles Root Certificate` [선택]
* `인증서 추가 | 로그인 | 추가` [선택]
  ![](/assets/images/2018-03-04/install-root-certificate.png)
* Charles의 인증서를 신뢰하는 인증서로 변경한다. `Charles Proxy` [선택]
  ![](/assets/images/2018-03-04/install-root-certificate2.png)
* `Charles Proxy CA | 항상신뢰` [선택]
  ![](/assets/images/2018-03-04/install-root-certificate3.png)
  ![](/assets/images/2018-03-04/install-root-certificate4.png)


## Install Charles Root Certificate on a Mobile Device or Remote Browser

> 기본적으로 Charls 어플리케이션 (Mac)과 같은 네트워크여야 한다.

* Install Charles Root Certificate on a Mobile Device or Remote Browser > [선택]
* 설정 > Wi-Fi > 정보 > 프록시 구성 > Charles IP, Port > [입력]
* Safari > chls.pro/ssl > [다운로드]
* 설정 > 일반 > 정보 > 인증서 신뢰 설정 > [활성화]

## 참고

* [Charles SSL Cetificates](https://www.charlesproxy.com/documentation/using-charles/ssl-certificates/)
