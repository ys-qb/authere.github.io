---
title: Git 터미널에서 제대로 사용하기- bash-git-prompt
categories:
  - Blog
  - Tool
thumbnail: https://www.evernote.com/l/AAWW2E0W9ldP_4yIGhmN9QeJqwtslwtU2LYB/image.png
date: 2017-10-22 09:49:25
tags:
  - git
  - terminal
  - osx
---

나는 오래된 개발자라 주로 맥이나 리눅스의 터미널에서 작업을 합니다. 따라서, 터미널에서 벗어 나지 않고 편하게 사용하도록 환경을 꾸며봅니다.

여러 feature 브랜치를 넘나들면서 사용하다 보면, 엄한 브랜치에서 commit 하는 실수가 잦은데요. 단순히 어느 branch에서 작업하고 있는지 command line에 표시만 해서 사용해서 더 이상의 실수를 줄일 수 있었습니다.
{% gist 3ca62ff35fbbe260f9150752f9e75376 %}

최근에는 좀 더 욕심이 생겨서, 원격`Remote`에 있는 저장소`repository`를 확인해서 다양한 정보를 보여주는 bash-git-prompt를 사용합니다.

https://github.com/magicmonty/bash-git-prompt

<!-- 기본 테마들도 훌륭한데요. 두 줄짜리 Solarized에서 Crunch 테마 변경해 봅니다.
{% asciinema wwQffkrpKPVIL3i26HzvPTLq8 %} --!>

기본 테마에 만족하지 못하고, 심플한 한 줄짜리로 만들어 봤습니다.

 - 원격`remote`에 push된 하나의 commit이 있음
 ![](https://www.evernote.com/l/AAWib19bJSJA-50rY_idU3euOxXAYAeduMsB/image.png)
 - staged: 1개, 수정된`changed`: 1개, untracked: 4개의 파일이 있음.
 ![](https://www.evernote.com/l/AAWW2E0W9ldP_4yIGhmN9QeJqwtslwtU2LYB/image.png)

## Step 1 
`~/.bashrc` 에 다음과 같이 추가하고,
{% gist 54cf7464d8712fd99f74669ac7188bbb .bashrc %}

혹은, 이렇게 바로 추가
```shell
$ gist -r 54cf7464d8712fd99f74669ac7188bbb .bashrc >> ~/.bashrc
```


## Step 2
~/.git-prompt-colors.sh 을 만들어 주세요. 직접 [Custom theme](https://github.com/magicmonty/bash-git-prompt/blob/master/themes/Custom.bgptemplate) 을 참고해서 만들거나, 한줄에 간단하게 표시되도록 만들어 둔 버전을 받으세요.
```shell
$ gist -r 54cf7464d8712fd99f74669ac7188bbb .git-prompt-colors.sh > ~/.git-prompt-colors.sh
```

---

## Trouble Shooting

### gist command line 도구 설치
터미널`terminal`에서 바로 github의 [gist](gist.gitub.com)를 바로 사용할 수 있는 도구를 이용합니다.
https://github.com/defunkt/gist

### `.bashrc` 의 내용이 적용이 안된다면
이유는 OSX의 터미널이 리눅스에서 xterm 수행할때와 다르게 동작하기 때문입니다. 자세한 이유는 여기에: [What is the difference between .bash_profile and .bashrc?](https://apple.stackexchange.com/questions/51036/what-is-the-difference-between-bash-profile-and-bashrc)

해결 방법은
 - `.bashrc` 파일은 사용하지 말고, `.bash_profile` 에 해당 내용을 추가
 - `.bash_profile` 에 `.bashrc` 읽도록 다음 추가.
 ```
if [ -f ~/.bashrc ]; then
  source ~/.bashrc
fi
 ```
