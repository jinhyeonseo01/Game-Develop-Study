# Git Rebase —i / —interactive

설명: Git Rebase를 통해 커밋 히스토리 수정하기

```bash
**git rebase -i ${수정할 커밋의 직전 커밋}**
```

> 명령어 뒤에 베이스 역할을 하는 브랜치 이름을 붙여 Rebase 절차를 진행할 수도 있지만, 해당 페이지에선 커밋 히스토리의 수정에 대해 설명합니다.
> 

**리베이스할 커밋의 직전 커밋**에는 내가 수정하고 싶은 커밋의 바로 직전 커밋을 입력하면 됩니다. 즉, 세번째 커밋을 수정하려한다면 두번째 커밋을 입력하면됩니다. 커밋 해시를 이용하거나 HEAD를 기준으로 입력할 수도 있습니다.

<aside>
⚠️ 협업하는 과정에서 이미 원격에 푸시된 커밋 히스토리를 리베이스하는 일은 지양해야합니다.
리베이스는 기존의 커밋을 재사용하는 것이 아닌, 내용이 같은 커밋을 만들기 때문에 협업자의 커밋 히스토리를 망가뜨릴 수도 있습니다.

</aside>

 예시

```bash
# 커밋 해시를 이용한 방법
git rebase -i 9d9cde8

# HEAD를 이용한 방법
git rebase -i HEAD~3
```

이렇게 입력하게되면, vim 에디터를 볼 수 있습니다.

 vim 에디터

```
pick a5806f4 세번째 커밋
pick 3bda4f0 네번째 커밋
pick 912ecc8 다섯번째 커밋

# Rebase acb0c25..09d4473 onto acb0c25 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

내용을 살펴보면 이렇습니다. **위에서부터 아래로** 커밋 순서가 출력되어 있으며, 각 라인은 `**[명령어]` `[커밋 해시]` `[커밋 메세지]`** 순서로 구성되어있습니다. vim을 종료시킬때, Git은 각 커밋에 적용시킬 명령어를 읽은 후 스크립트를 한줄씩 진행시킵니다.

아래 주석은 각 커밋에 사용할 수 있는 명령어들의 목록입니다. 즉, 특정 커밋에 명령어를 사용하기 위해서는 직접 vim 에디터로 커밋 해시 앞 명령어의 내용을 수정해야합니다.

 예시. 네번째 커밋에 edit 명령어를 적용

```
pick a5806f4 세번째 커밋
edit 3bda4f0 네번째 커밋
pick 912ecc8 다섯번째 커밋

# Rebase acb0c25..09d4473 onto acb0c25 (2 commands)
#
# Commands:

...

# However, if you remove everything, the rebase will be aborted.
#
```

<aside>
💡 vim 에디터에서 메세지를 수정하는 경우에는 `i키`를 눌러 INSERT 모드로 들어갈 수 있으며, 메세지 수정 후 `Esc키`를 누른 후 `:wq`를 입력해 저장후 종료할 수 있습니다.

</aside>

---

# 명령어 목록

## pick - 유지, 커밋 순서 변경, 커밋 삭제

<aside>
🔄 **커밋 순서 변경**
`pick` 3bda4f0 네번째 커밋
`pick` a5806f4 세번째 커밋
pick 912ecc8 다섯번째 커밋

</aside>

<aside>
🗑️ **커밋 삭제**
pick a5806f4 세번째 커밋
pick 912ecc8 다섯번째 커밋

</aside>

`pick` 또는 `p`는 **해당 커밋을 수정하지 않고 그냥 사용하겠다라는 명령어** 입니다. 기본값으로 설정되어있으므로 vim을 내용을 편집하지 않고 종료한다면 아무런 변경 사항 없이 rebase가 종료됩니다. 

이런 특성을 통해 pick의 순서를 변경하여 **커밋 순서를 재정렬**하거나 아예 **커밋을 삭제**할 수 있습니다.

## reword - 커밋 메세지 수정

<aside>
✏️ **커밋 메세지 수정**
pick a5806f4 세번째 커밋
****`reword` 3bda4f0 네번째 커밋 (reword로 수정)
pick 912ecc8 다섯번째 커밋

</aside>

`reword` 또는 `r` 는 **커밋 메시지를 수정하기 위한 명령어**입니다.

## edit - 커밋의 명령어 및 작업 내용 수정

 커밋 메세지, 작업 내용 수정 및 커밋 분리, 결합

```
pick a5806f4 세번째 커밋
****edit 3bda4f0 네번째 커밋
pick 912ecc8 다섯번째 커밋
```

`edit` 명령어를 네번째 커밋에 사용하게되면, 해당 네번째 커밋으로 HEAD가 이동합니다.

```bash
git on master took 2m 7s
Stopped at 3bda4f0... 네번째 커밋
You can amend the commit now, witlose the file...

	git commit --amend

Once you are satisfied with your changes, run

	git rebase --continue

git on (git)-[master|rebase-i]- took 14m 8s
```

해당 네번째 커밋으로 HEAD가 옮겨진 것을 확인할 수 있습니다. 가운데 설명은 커밋 메세지를 수정하려면 `git commit —amend`를, 수정을 완료했다면 `git rebase —continue` 명령어를 입력하라는 내용입니다.

 커밋 메세지를 수정하기 위해 `git commit —amend`를 입력한 경우

```bash
네번째 커밋

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date :         Thu Apr 20 18:18:52 2023 +0900
#
# interactive rebase in progress: onto ab44144
-- INSERT --
```

`reword` 명령어를 사용했을때와 마찬가지로, 커밋 메세지를 수정할 수 있는 vim 에디터가 뜹니다. 동일한 방식으로 수정할 수 있습니다.

 네번째 커밋(현재 커밋)과 다섯번째 커밋 사이에 추가적인 작업을 진행하기

4.5.txt 텍스트 파일 생성 후, `git add`와 `git commit -m message`명령어를 통해 새 커밋 생성한 상태입니다.

- `git log` 실행시
    
    ```bash
    commit 3487d705defe550e4792bc0babf8408bafaf77eb (HEAD)
    Author: yourname <yourname@yourmail.com>
    Date:   Thu Apr 20 18:26:22 2023 +0900
    
        네번째와 2분의 1 승강장 커밋
    
    commit 3bda4f0qngk849eh6589jr98gkw54891re6h
    Author: yourname <yourname@yourmail.com>
    Date:   Mon Jul 16 23:19:26 2012 +0900
    
        네번째 커밋
    
    commit a5806f4ae894e4h41h584894rh1651n56t44rt68
    Author: yourname <yourname@yourmail.com>
    Date:   Mon Jul 16 23:19:01 2012 +0900
    
        세번째 커밋
    ```
    

신규 커밋이 네번째 커밋 뒤에 추가된 것을 확인할 수 있습니다.
이제 네번째 커밋에서 할 일이 끝났으니, `git rebase —continue`로 진행 중인 rebase 과정을 종료해보겠습니다.

 

 `git rebase —continue` 실행

```
commit 912ecc8wg5w1g610r56h5rwt151g5w15g1w5w58 (HEAD)
Author: yourname <yourname@yourmail.com>
Date:   Thu Apr 20 18:26:22 2023 +0900

    다섯번째 커밋

commit 3487d705defe550e4792bc0babf8408bafaf77eb
Author: yourname <yourname@yourmail.com>
Date:   Thu Apr 20 18:26:22 2023 +0900

    네번째와 2분의 1 승강장 커밋

commit 3bda4f0qngk849eh6589jr98gkw54891re6h
Author: yourname <yourname@yourmail.com>
Date:   Mon Jul 16 23:19:26 2012 +0900

    네번째 커밋

commit a5806f4ae894e4h41h584894rh1651n56t44rt68
Author: yourname <yourname@yourmail.com>
Date:   Mon Jul 16 23:19:01 2012 +0900

    세번째 커밋
```

네번째 커밋과 다섯번째 커밋 사이에 신규 커밋이 추가되었습니다.

## squash, fixup - 커밋 합치기

<aside>
🍐 **커밋 두개 합치기**
pick 3bda4f 네번째 커밋
****`squash / fixup` 3487d7 네번째와 2분의 1 승강장 커밋
pick 912ecc8 다섯번째 커밋

</aside>

`squash` 와 `s` , `fixup` 과 `f` 는 **해당 커밋을 이전 커밋과 합치는 명령어**입니다.

다만, 두 명령어 사이에는 차이점이 있습니다. `squash` 는 각 커밋들의 메세지가 합쳐지는 반면, `fixup` 은 이전의 커밋 메세지만 남겨지게됩니다.

 `squash`를 통해 커밋 합치는 경우

```
# This is a combination of 2 commits.
# This is the 1st commit message:

네번째 커밋

# This is the commit message #2:

네번째와 2분의 1 승강장 커밋

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date :         Fri Apr 11:40:53 2023 +0900
```

네번째 커밋과 네번째와 2분의 1 승강장 커밋의 메세지를 확인할 수 있습니다. 필요에 따라 커밋 메세지를 수정할 수도 있습니다.

- `git log` 실행시
    
    ```bash
    commit 912ecc8wg5w1g610r56h5rwt151g5w15g1w5w58 (HEAD)
    Author: yourname <yourname@yourmail.com>
    Date:   Thu Apr 20 18:26:22 2023 +0900
    
        다섯번째 커밋
    
    commit 3487d705defe550e4792bc0babf8408bafaf77eb
    Author: yourname <yourname@yourmail.com>
    Date:   Thu Apr 20 18:26:22 2023 +0900
    
        네번째 커밋
    
        네번째와 2분의 1 승강장 커밋
    
    commit a5806f4ae894e4h41h584894rh1651n56t44rt68
    Author: yourname <yourname@yourmail.com>
    Date:   Mon Jul 16 23:19:01 2012 +0900
    
        세번째 커밋
    ```
    

 `fixup`를 통해 커밋 합치는 경우

이전의 커밋인 네번째 커밋 메세지만 남게됩니다.

- `git log` 실행시
    
    ```bash
    commit 912ecc8wg5w1g610r56h5rwt151g5w15g1w5w58 (HEAD)
    Author: yourname <yourname@yourmail.com>
    Date:   Thu Apr 20 18:26:22 2023 +0900
    
        다섯번째 커밋
    
    commit 3487d705defe550e4792bc0babf8408bafaf77eb
    Author: yourname <yourname@yourmail.com>
    Date:   Thu Apr 20 18:26:22 2023 +0900
    
        네번째 커밋
    
    commit a5806f4ae894e4h41h584894rh1651n56t44rt68
    Author: yourname <yourname@yourmail.com>
    Date:   Mon Jul 16 23:19:01 2012 +0900
    
        세번째 커밋
    ```
    

## exec - 리베이스 과정 중에 쉘 커멘드 실행하기

<aside>
📢 **쉘 커멘드 실행하기**
pick 3bda4f 네번째 커밋
`exec` git log -1 —pretty=format:%B
****pick 3487d7 네번째와 2분의 1 승강장 커밋
`exec` git log -1 —pretty=format:%B
pick 912ecc8 다섯번째 커밋

</aside>

`exec` 는 **리베이스 도중 쉘 커멘드를 실행할 수 있게 해주는 명령어**입니다.

- 리베이스 과정 실행시
    
    ```bash
    Executing: git log -1 --pretty=format:%B
    네번째 커밋
    Executing: git log -1 --pretty=format:%B
    네번째와 2분의 1 승강장 커밋
    Successfully rebased and updated refs/heads/master.
    ```
    

`Executing` 으로 실행할 명령어가 나오고 결과가 출력됩니다.

## break - 리베이스 과정 일시중지하기

<aside>
🛏️ **리베이스 일시중지**
pick 3bda4f 네번째 커밋
****pick 3487d7 네번째와 2분의 1 승강장 커밋
`break`
pick 912ecc8 다섯번째 커밋

</aside>

`break`는 **리베이스 도중 쉘 커멘드를 실행할 수 있게 해주는 명령어**입니다.

단순히, 해당 라인까지 리베이스를 마친 후 일시중지한 상태가 되며, 재개하려면 `git rebase —continue` 를 입력하면 됩니다.

## break - 리베이스 과정 일시중지하기

<aside>
🗑️ **커밋 삭제하기**
pick 3bda4f 네번째 커밋
****`drop` 3487d7 네번째와 2분의 1 승강장 커밋
pick 912ecc8 다섯번째 커밋

</aside>

`drop`은 **해당 커밋을 명시적으로 삭제하는 명령어**입니다.

`pick` 을 이용하여 삭제하는 방식과 동일한 결과가 나오게됩니다.

## merge - 머지 커밋 생성하기

<aside>
🗑️ **커밋 삭제하기**
pick 3bda4f 네번째 커밋
****pick 3487d7 네번째와 2분의 1 승강장 커밋
pick 912ecc8 다섯번째 커밋
`merge` a627eh

</aside>

`merge`는 **머지 커밋을 만들면서 머지하는 명령어**입니다.

 다른 브랜치에서 작업한 `a627eh` 머지하기

```bash
Merge branch 'a627eh'
#
# It looks like you may be committing a merge.
# If this is not correct. please remove the file
#         .git/MERGE_HEAD
# and try again.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date :         Thu Apr 20 18:18:52 2023 +0900
#
# interactive rebase in progress: onto ab44144
-- INSERT --
```

해당 라인에서 vim 에디터가 열려서 머지 커밋을 작성할 수 있게됩니다.