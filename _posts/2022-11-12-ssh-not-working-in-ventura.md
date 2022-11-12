---
title: "Mac Ventura 에서 SSH 접속 안될때"
categories: mac  
tags: mac
---

> Mac OS Ventura로 업데이트 하고 나서 잘 사용하던 SSH가 동작하지 않는다.

## 해결방법

* `/etc/ssh/ssh_config` 수정 마지막에 아래 내용 추가

```shell
sudo vi /etc/ssh/ssh_config

...
    HostkeyAlgorithms +ssh-rsa
    PubkeyAcceptedAlgorithms +ssh-rsa
```

* 전체 설정

```shell
#       $OpenBSD: ssh_config,v 1.35 2020/07/17 03:43:42 dtucker Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1. command line options
#  2. user-specific file
#  3. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# This Include directive is not part of the default ssh_config shipped with
# OpenSSH. Options set in the included configuration files generally override
# those that follow.  The defaults only apply to options that have not been
# explicitly set.  Options that appear multiple times keep the first value set,
# unless they are a multivalue option such as IdentityFile.
Include /etc/ssh/ssh_config.d/*

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

# Host *
#   ForwardAgent no
#   ForwardX11 no
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   IdentityFile ~/.ssh/id_ecdsa
#   IdentityFile ~/.ssh/id_ed25519
#   Port 22
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
#   RekeyLimit 1G 1h
#   UserKnownHostsFile ~/.ssh/known_hosts.d/%k
Host *
    SendEnv LANG LC_*
    HostkeyAlgorithms +ssh-rsa
    PubkeyAcceptedAlgorithms +ssh-rsa
```

## 참고

* [SSH not working in macOS Ventura: How to Fix](https://www.droidwin.com/ssh-not-working-in-macos-ventura-fix/)