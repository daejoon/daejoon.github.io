---
title: "Mac에서 Docker를 Podman으로 대체해보기 추가적으로 IntelliJ IDEA 호환성 유지"
categories: intellij docker
tags: mac m1 docker podman
---

> 개인이 사용시에는 Docker-Desktop(이하 Docker)이나 Podman-Desktop(이하 Podman) 둘중 편한것으로 선택하면 됩니다.
> Docker는 회사에서 사용하면 회사 규모에 따라서 [라이센스](https://www.docker.com/pricing/)가 필요합니다.
> 개인이 사용하는데 무료이지만 점점 사이트 로그인도 필요하고 강제하는 부분이 늘어나서 이번기회에 Podman으로 변경하였습니다.
>
> 변경하면서 제일 걱정이 되는 부분은 IntelliJ-IDEA와의 호환성이 이었습니다.
> 개인적으로 대부분 작업을 IntelliJ-IDEA 한곳에서 작업을 진행합니다.
> Docker를 구동시키면 View > Tool Windows > Service에서 확인 하는데 이분도 같이 해결되면 좋겠다는 생각을 했습니다.

아래는 Podman으로 대체 방법입니다.

## Brew 설치

* 기존에 설치되어 있다면 건너뛰면 됩니다.

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Podman 설치

* podman-compose도 같이 설치 해 줍니다.

```shell
brew install podman-desktop podman-compose
```

## Podman 설정

* Docker Compatibility Enable
    * Docker와 호환성을 위해서 활성화 합니다.

![](/assets/images/2024-09-25/docker-compatibility-enable.png)

* Registries 에서 기존 Docker Hub 계정 등록
    * docker pulling시 이용 됩니다.

![](/assets/images/2024-09-25/docker-registries.png)

## Docker 호환성 유지를 위한 심볼릭 추가

* 기존 Docker 명령어 그대로 사용하기 위해서 심볼릭 링크를 추가 합니다.

```shell
sudo ln -s $(which podman) /usr/local/bin/docker
sudo ln -s $(which podman-compose) /usr/local/bin/docker-compose
sudo ln -s /Users/$USER/.local/share/containers/podman/machine/podman.sock /var/run/docker.sock
```

## IntelliJ IDEA > Docker 설정

* 이름 변경
    * 이름 변경은 필수가 아닙니다. 기존 Docker와 구별을 위해서 변경했을 뿐 입니다. 그대로 사용해도 무방 합니다.

![](/assets/images/2024-09-25/intellij-idea-podman.png)

* 서비스 연결 확인

![](/assets/images/2024-09-25/intellij-idea-services.png)

## 참고

* [Homebrew Homepage](https://brew.sh/)
* [Jetbrains Rider Podman](https://www.jetbrains.com/help/rider/Podman.html)
* [Using the podman-mac-helper tool to migrate from Docker to Podman on macOS](https://podman-desktop.io/docs/migrating-from-docker/using-podman-mac-helper)
* [Troubleshooting Podman on macOS](https://podman-desktop.io/docs/troubleshooting/troubleshooting-podman-on-macos)