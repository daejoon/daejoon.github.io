---
title: "IntelliJ 저장시 Reformat과 Imports 정리"
categories: intellij  
tags: intellij mac
---

> 작업을 하면서 저장을 하다 보면은 format이나 사용하지 않는 imports 파일이 포함되어 커밋할때가 있다.
> 물론 Git Commit 전에 훅으로 정리할수 있지만 나중에 확인하면 내가 수정하지 않은 부분 까지 Reformat이 되면서
> 코드 리뷰하거나 확인할때 당황하게 되어서 난 잘 사용하지 않게 된다. 그리고 너무 많은 사항이 발생하면 리뷰를 하기 힘들어진다.
> 그래서 나는 되도록이면 Imports는 Commit 전에 단축크로 정리하고 AutoFormat은 사용하지 않는데
> 해당 옵션을 사용하면은 필요한 부분만 자동으로 변경되어서 그나마 낫다고 생각이 든다.

## 옵션 설정

### 기본 설정

* 위치
    * `Preferences` > `Tools` > `Actions on Save`

![기본](/assets/images/2022-03-20/default.png)

### 변경 설정

![설정](/assets/images/2022-03-20/after.png)

* 해당 설정은 각 Project 별로 설정 해야 한다.
* 변경 라인만 Reformat 하면은 나중에 리뷰 할때 덜 당황한다.
* 사용하지 않는 Imports는 자바의 경우 나중에 컴파일할때 오류가 발생할수 있으니 미리미리 정리 해주는게 좋다.
