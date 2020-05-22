---
title: "remote: HTTP Basic: Access denied"
categories: git
tags: git
---

## 목표
> 로그인 정보가 일치하지 않을때 발생하는데 이럴때는 초기화 시키고 다시 설정하는 것이 편하다.

## SYNOPSIS
```
git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] name [value [value_regex]]
       git config [<file-option>] [--type=<type>] --add name value
       git config [<file-option>] [--type=<type>] --replace-all name value [value_regex]
       git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] --get name [value_regex]
       git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] --get-all name [value_regex]
       git config [<file-option>] [--type=<type>] [--show-origin] [-z|--null] [--name-only] --get-regexp name_regex [value_regex]
       git config [<file-option>] [--type=<type>] [-z|--null] --get-urlmatch name URL
       git config [<file-option>] --unset name [value_regex]
       git config [<file-option>] --unset-all name [value_regex]
       git config [<file-option>] --rename-section old_name new_name
       git config [<file-option>] --remove-section name
       git config [<file-option>] [--show-origin] [-z|--null] [--name-only] -l | --list
       git config [<file-option>] --get-color name [default]
       git config [<file-option>] --get-colorbool name [stdout-is-tty]
       git config [<file-option>] -e | --edit
```

## Options
```
--system
           For writing options: write to system-wide $(prefix)/etc/gitconfig
           rather than the repository .git/config.

           For reading options: read only from system-wide
           $(prefix)/etc/gitconfig rather than from all available files.

           See also the section called "FILES".
--unset
           Remove the line matching the key from config file.
```

## CONFIGURATION FILE
```
credential.helper
           Specify an external helper to be called when a username or password
           credential is needed; the helper may consult external storage to
           avoid prompting the user for the credentials. Note that multiple
           helpers may be defined. See gitcredentials(7) for details.
```
## 초기화
```
git config --system --unset credential.helper
```

## 계정 정보 저장
```
git config credential.helep store
```
