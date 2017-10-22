---
title: Git - 리누스 토발즈가 만든 클라우드 시대의 버전 관리 도구 
date: 2017-10-21 18:02:26
tags: 
  - git
  - tool
  - linux
categories:
  - Blog
  - Tool
thumbnail: /images/Git-logo.svg
---

리눅스 커널은 가장 복잡하고 많은 사람이 참여하여 공동작업한 오픈소스 소프트웨어 중의 하나입니다. 리눅스의 창시자이자인 리누스 토발즈`Linus Torvalds`는 리눅스 커널 소스코드의 관리의 어려움을 해결해 줄 수 있는 오픈소스로 된 버전관리 도구가 필요했는데 마땅한 것이 없었답니다. 그래서, 직접 Git을 개발하게 되었다고 합니다.

Github에 미러되어 있는 Linus Torvalds의 git 소스코드의 [첫번째 변경`commit`](https://github.com/git/git/commit/e83c5163316f89bfbde7d9ab23ca2e25604af290)을 구경해 보세요~

{% blockquote Linus Torvalds, Git source code repo %}
Initial revision of "git", the information manager from hell
{% endblockquote %}

![](https://www.evernote.com/l/AAUKFtn9xfZA1LeISQLMfDyq_-2A-oQU-w8B/image.png)


출생 배경이 이런지라, 
 - Git 대규모 소스 코드의 분산 관리에 능하고, 중복제거 압축등으로 저장공간도 효율적으로 사용합니다.
 - 공동작업시 서로의 변경사항이 발생해도 대부분의 경우 자동으로 병합`Merge`해 줍니다. 
 - 간혹 한 파일의 같은 부분을 동시에 수정하게 되면 충돌`Conflict`이 나지만, 대부분의 경우 한 파일내에 다른 부분을 동시에 수정하더라도 자동으로 병합`Auto Merge`됩니다.

들어가는 말은 이정도로 하고, 다음 포스팅 부터는 일상적인 도구로 활용하는 이야기를 해 보겠습니다.
