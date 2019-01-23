---
title: "Python virtualenv"
date: 2016-05-15 01:00:00 +0900
categories: python
---

Python은 개발시 라이브러리 충돌을 피하기 위해서 virtual environment를 구성할수 있습니다.

virtual environment 구성하면 생성 및 삭제가 편해집니다.

## 사용방법

- 우선 virtual enviroment을 설치합니다.
  ```
  $ pip install virtualenv
  ```
- 해당 프로젝트 폴더로 이동한다.
  ```
  $ virtualenv venv
  ```
- virtual enviroment 환경으로 전환한다.
  ```
  $ source venv/bin/activate
  ```
- 그럼 mac 기준으로 아래와 같이 표시된다.
  ```
  $ (venv) KDJ-MBP:LearningSQLAlchemy kdj$
  ```
- virtual enviroment를 종료하는 방법은 `deactivate`을 호출하면 된다.
  ```
  $ deactivate
  ```
- virtual enviroment 환경에서 패키지를 다운로드 하거나 설치하는것은 글로벌과 별게로 설치된다.
