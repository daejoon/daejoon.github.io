---
title: git difftool
date: 2016-12-17 12:00:00 +0900
categories: git
---

git 명령어에는 익숙해지려고 하지만 git의 기본 `diff`는 개인적으로 보기 힘들다.

그래서 외부 툴을 사용한다.

Mac [Kaleidospce](http://www.kaleidoscopeapp.com/)라는 앱을 사용중이다.

## .gitconfig
```
...
[merge]
	tool = Kaleidoscope
[mergetool "Kaleidoscope"]
	cmd = ksdiff --merge --output \"$MERGED\" --base \"$BASE\" -- \"$LOCAL\" --snapshot \"$REMOTE\" --snapshot
	trustexitcode = true
[diff]
	tool = Kaleidoscope
[difftool "Kaleidoscope"]
	cmd = ksdiff --partial-changeset --relative-path \"$MERGED\" -- \"$LOCAL\" \"$REMOTE\"
[difftool]
	prompt = false
[mergetool]
	prompt = false
...
```

`ksdiff`는 `Kaleidoscope`의 command line tool 이다.

## IntelliJ IDEA

다음 내가 주력으로 사용하는 IntelliJ IDEA의 diff 설정도 변경한다.

이동 `Preferences ...`->`Tools`->`Diff & Merge`->`External Diff Tools`


### Diff tool 설정

Use external diff tool -> [check]

Use by default -> [check]

Path to executable: `/usr/local/bin/ksdiff`

Parameter: `-- %1 %2`

### Merge tool 설정

Use external merge tool: [check]

Trust process exit code: [check]

Path to executable: `/usr/local/bin/ksdiff`

Parameter: `--merge --output %4 --base %3 -- %1 --snapshot %2 --snapshot`


%1: left (Loacl changes)

%2: right (Server content)

%3: base (Current version without local changes)

%4: output (Merge result)




