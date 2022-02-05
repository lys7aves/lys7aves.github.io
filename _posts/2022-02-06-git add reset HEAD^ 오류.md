---
layout: post
title: 'git reset HEAD^ 오류'
date: 2022-02-06
author: 이유섭
cover: 'https://images.unsplash.com/photo-1465189684280-6a8fa9b19a7a?w=1600&q=900'
tags: git github commit reset HEAD HEAD^
---



# commit 취소

git commit 을 취소하고자 할 때, 다음과 같은 명령어를 통해 취소를 할 수 있다.

```bash
$ git reset HEAD^
```



# git reset HEAD^ 오류

그러나 위의 명령어를 입력하자 다음과 같이 More? 라는 문구가 뜨며 추가적인 입력을 요구했다.

```bash
$ git reset HEAD^
More?
```

여기서 아무것도 입력하지 않으면 아마 다음과 같은 에러가 뜰 것이다.

```bash
fatal: ambiguous argument 'HEAD
': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
```



찾아보니 Windows 쉘에서 ^를 문자 그대로 받아들이지 않고 추가적인 입력이 있다는 기호로 받아들이기 때문이었다.

이를 해결하기 위해선 다음과 같은 2가지 방법이 있다.

1. ```bash
   $ git reset HEAD^
   More? ^
   ```

   More? 가 떴을 때, ^를 추가로 입력하여 명령어를 완성해준다.

2. ```bash
   $ git reset HEAD^^
   ```

   처음부터 ^를 한번 더 써 준다.



# 첫 commit 취소 오류

위의 방법을 다 따라 했는데도 불구하고 나는 계속 아래와 같은 오류가 발생하였다.

```bash
fatal: ambiguous argument 'HEAD^': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'
```

나는 이 오류가 되돌아갈 commit이 없어서 뜬 것이라고 판단하였다. (아니라면 알려주세요)



나의 경우 기존의 repository에서 처음 해보는 것을 하기가 무서워 새로운 test repository를 만들어서 실험해보고 있었다.

자연스레 commit을 한번 하고 이 commit을 취소하려고 하였고 계속해서 위와 같은 오류에 부딪히게 되었다.

부족한 서칭 실력으로 열심히 검색해보았지만 해결책을 찾지 못했고, 이것저것 테스트 하다 commit을 한번 더 하니 위의 오류가 뜨지 않는 것을 확인할 수 있었고, commit log가 하나인 상태에서는 더 이상 취소가 안된다는 것을 알 수 있었다.



따라서 나는 첫 commit 의 경우 취소가 불가하다고 판단하였다.

첫 commit의 경우  commit 을 쌓아온 것이 없기에 .git 폴더를 지우고 다시 add 와 commit을 해도 별 차이 없어 그러지 않을까라고 생각하였다.

(혹시 첫 commit 도 취소할 수 있는 방법이 있다면 알려주세요 ㅎㅎ)



현재 commit log를 보고 싶다면 아래의 명령어를 입력해주면 된다.

```bash
$ git log
```

또한 아래와 같이 git log를 했을 때 오류가 뜨는 것은 git reset 을 해도 오류가 뜨는 것 같다.

```bash
$ git log HEAD^
# HEAD^ 대신 HEAD나 HEAD~1, HEAD~2 등을 쓸 수도 있다.
```
