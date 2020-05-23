---
title: "Gitlab remote: HTTP Basic: Access denied"
categories: git
tags: git gitlab
---

## 목표
> 로그인 정보가 일치하지 않을때 발생한다. 계정 정보를 초기화 하고 재 설정 한다.

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
$ git config --system --unset credential.helper
```

## Git push
```
$ git push
```
- `ID`, `PASSWORD`를 입력

## 계정 정보 저장
```
$ git config credential.helep store
```
- ID, PASSWORD를 저장한다.
