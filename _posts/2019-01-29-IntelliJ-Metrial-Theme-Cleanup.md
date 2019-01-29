---
title: IntelliJ IDEA의 Metrial UI Theme 지우기
categories: intellij
---

`IntelliJ IDEA`의 플러그인중에 [Metrial UI Theme](https://github.com/ChrisRM/material-theme-jetbrains)가 있다. 이 플러그인을 설치하면 다양한 테마로 UI를 변경할수 있다. 다만 설치할때는 좋은데 설치하고 나서 플러그인을 제거해도 원래 테마(`Darcula`)로 돌아오지 않는 버그가 있다.

돌아오지 않는다는게 완전히 다른 테마가 되는건 아니고 VCS 폰트 색상이 Custom되는 버그 이다.
아래 이미지를 확인하면 `* Customized`라고 표시된걸 확인할 수 있다.

![](/assets/images/Preferences-2019-01-29-17-00-00.png)

## 해결방법
- 플러그인을 제거(Uninstall) 한다.
- [Plugin Setting 제거](https://intellij-support.jetbrains.com/hc/en-us/articles/206544519-Directories-used-by-the-IDE-to-store-settings-caches-plugins-and-logs)을 참고하여 설정중 `Metrial UI Theme`의 설정만 제거 한다.
- **마지막으로 가장중요한** Custom Font 제거
- Library > Preferences > IntelliJIdea2018.3 > jba_config > colors > 아래의 `_@user_Darcula.icls`, `_@user_Default.icls` 제거
- 파일은 테마에 따라서 다르게 생성될수 있다.

## 제거된 모습
![](/assets/images/Preferences-2019-01-29-17-50-44.png)
