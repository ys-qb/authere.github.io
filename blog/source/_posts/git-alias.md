---
title: Git 터미널에서 제대로 사용하기 - alias
categories:
  - Blog
  - Tool
thumbnail: https://www.evernote.com/l/AAVdh-x4ooxAN6bubLW460BwLqMuRfazMngB/image.png
date: 2017-10-22 16:41:08
tags:
  - git
  - terminal
  - osx
---

일상적으로 사용하는 git command 를 쓰기편하게도록 alias를 지정해서 사용합니다.

alias 지정방법은 
 - `~/.gitconfig` 의 alias section에 바로 추가해도 되고,
 - `git config --global alias.co checkout` 요렇게 수행해도 됩니다.

```ini ~/.gitconfig
[alias]
  co = checkout
  ci = commit
  cia = commit --amend
  st = status
  br = branch
  sdiff = diff --staged
  hdiff = diff HEAD
  go = "!f() { git checkout -b \"$1\" 2> /dev/null || git checkout \"$1\"; }; f"
  p2g = "!f() { git diff HEAD --no-prefix | gist -p -f patch_`date +%Y%m%d`.patch; }; f"
  g2p = "!f() { gist -p -r \"$1\" 2> /dev/null | patch -p0 ; }; f"
  rh = reset --hard HEAD    #rest hard
  rhc = "!f() { git reset --hard HEAD && git clean -fd; }; f"
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
```

## cia - commit --amend

바로 전 commit에 빠진 부분이 있거나 comment를 변경하려고, push 하기전에 바로 전 commit에다가 변경을 가하는 것입니다. 이미 push를 했다면 포기하는 것이 좋습니다.[How do I push amended commit to the remote Git repository?
](https://stackoverflow.com/questions/253055/how-do-i-push-amended-commit-to-the-remote-git-repository)

## sdiff, hdiff

![](https://i.stack.imgur.com/tVHYO.png)
출처: https://stackoverflow.com/questions/1587846/how-do-i-show-the-changes-which-have-been-staged

`git diff` 는 staged(cached와 동일) 되지 않은 수정만 보여 줍니다.
sdiff 는staged된 것과 HEAD(현재 commit된 최신 버전)의 차이을 보여 줍니다.
hdiff 는 모든 변경(staged 됐든 말든)과 HEAD의 차이를 보여 줍니다.

## go branch_name

branch 가 없으면, 만들고 있으면 switch합니다.

## p2g, g2p 

아직 commit할 단계는 아니지만, 작업을 저장하고 싶을 때는 `stash`를 이용합니다. 여러 개발 machine을 오가면서 사용하다 보면, 현재 상태를 원격으로 공유해야 할 때가 있습니다. stash를 remote branch로 만드는 방법이 있습니다. [How can I share a git stash?](https://superuser.com/questions/409228/how-can-i-share-a-git-stash)

나는 gist 에 패치파일을 올려 두고 공유합니다. 현재 작업 중인 내용으로 patch 파일을 만들고, 이것을 gist 에 올립니다. 다른 machine에서 gist의 patch file을 가져와서 patch 적용합니다.

untracked file들은 저장되지 않으므로, `git add`해야함을 잊지 마세요.

## rh, rhc
rh 는 모든 변경 사항을 버립니다. 이때 untracked files는 정리되지 않는데, rhc는 이것들을 정리해 줍니다.
오랜시간했던 작업을 날릴 수 있으므로 주의해야 합니다.

---

git 으로 복잡한 소스코드를 관리하는 것은 상당히 머리 아픈 일입니다. 좀 더 직관적으로 복잡한 문제를 풀기위해 command line 도구만을 고집하지 않습니다. `stash`, `cherry-pick`, `manual merge` 등의 작업을 할 때는 [Sourcetree](https://www.sourcetreeapp.com/)를 사용합니다.

Sourcetree 메뉴에서, `Sourcetree -> Install Command Line Tools` 하고는 어디서나 `stree` 명령으로 수행합니다.
```
$ stree
```
