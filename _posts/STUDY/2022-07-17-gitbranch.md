---
layout: single
title: "Git Branch"
categories:
  - STUDY
tags:
  - [2022-07, STUDY, GIT]
sidebar:
  nav: "docs"
---

<center>
<img width="90%" src="./../../images/gitgit.png">
</center>
<br>

# <a style="color:#00adb5">Git Branch</a>

## <a style="color:#00adb5">Branch</a>

<big>Branch</big>
나뭇가지라는 의미로 여러 갈래로 작업 공간을 나누어 <a style="color:red"><strong>독립적으로 작업</strong></a>할 수 있도록 도와주는 GIT의 도구이다.<br>
버전 관리의 꽃이다 !<br>

## <a style="color:#00adb5">Branch 사용해야 하는 이유</a>

- master branch는 상용을 의미한다. 공개되어 있는 것 !
- 만약 상용에 에러가 있어서 고쳐야 한다면 ?
- 고객들이 사용하고 있는데 상용을 함부러 고치거나 삭제하면 안된다.
- 그래서 새로운 branch를 파서 ( master와 독립적으로 ) 고치고 master에 반영하면 된다.
- 새로운 branch에서 작업하는 동안 master에 아무런 영향을 끼치지 않는다.
- 이러한 이유로 branch는 Git에서 가장 강력한 기능 중 하나이다.

## <a style="color:#00adb5">Branch 장점</a>

- 독립 공간을 형성하기 때문에 <big>원본 ( master ) 에 대해 안전</big>
- 하나의 작업은 하나의 브랜치로 나누어 진행되므로 <big>체계적인 개발</big>이 가능
- 특히나 Git의 브랜치는 <big>굉장히 가벼우며</big> 순식간에 브랜치를 새로 만들고 브랜치 사이를 이동할 수 있다.

## <a style="color:#00adb5">Branch Command</a>

### <a style="color:#00adb5">git branch</a>

<a style="color:red"><strong>브랜치 조회, 생성, 삭제 등 브랜치와 관련된 Git 명령어</strong></a>

```bash
# 브랜치 목록 확인
$ git branch

# 원격 저장소의 브랜치 목록 확인
$ git branch -r

# 새로운 브랜치 생성
$ git branch <브랜치 이름>

# 특정 브랜치 삭제
$ git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
$ git branch -D <브랜치 이름> # 강제 삭제 ( 병합되지 않은 브랜치도 삭제 가능 )
```

### <a style="color:#00adb5">git switch</a>

<a style="color:red"><strong>브랜치 이동</strong></a>

```bash
# 다른 브랜치로 이동
$ git switch <다른 브랜치 이름>

# 브랜치를 새로 생성과 동시에 이동
$ git switch -c <브랜치 이름>
```

**git switch 주의사항**

> 'git switch' 하기 전에, 워킹 디렉토리 파일이 모두 버전 관리가 되고 있나 ?

- master branch와 featuer branch가 있다고 가정해보자
- feature branch에서 test.txt를 만들고 git add 하지 않은 상태에서 git switch master를 하면 어떤 일이 발생할까 ?
- master branch에도 test.txt가 생성된다.
  <br>
- 왜냐하면 Git branch는 독립적인 작업 공간을 가지지만, 어디까지나 git이 관리하는 파일 트리에 한애서만이다.
- 그래서 git add 를 하지 않은 새 파일은 브랜치가 바뀌더라도 계속 유지되는 것이다.
- 그래서 git switch를 하기 전에 항상 모든 워킹 디렉토리의 파일이 버전 관리가 되고 있는지 확인해야 한다.

### <a style="color:#00adb5">git merge</a>

<a style="color:red"><strong>브랜치 작업이 끝나고 Merge라고 하는 병합하기</strong></a><br>
분기된 브랜치들을 하나로 합치는 명령어

- **Merge 하기 전에 다른 브랜치를 합치려고 하는, 즉 메인 브랜치로 switch 해야 한다 !!**
- 기준이 되는 branch로 가서 merge를 한다.

```bash
# 1. 현재 branch1과 branch2 가 있고, Head가 가리키는 곳은 branch1 이다.
$ git branch
* branch1
  branch2

# 2. branch2를 branch1에 합치려면?
$ git merge branch2

# 3. branch1을 branch2에 합치려면?
# branch2로 이동해서 merge 하기
$ git switch branch2
$ git merge branch1

```

### <a style="color:#00adb5">git restore</a>

<a style="color:red"><strong>파일 내용을 수정 전으로 되돌리기</strong></a><br>

```bash
# 되돌리기
$ git restore test.txt
```

### <a style="color:#00adb5">파일 상태를 Unstage로 되돌리기</a>

- git add를 통해서 파일을 Staging Area에 올렸다고 가정
- 기존 커밋이 없는 경우
  - `git rm --cached <file> `
  - “to unstage and remove paths only from the staging area”
- 기존에 커밋이 존재하는 경우
  - `git restore --staged <file>`
  - “the contents are restored from HEAD”

### <a style="color:#00adb5">바로 직전 완료한 커밋 수정하기</a>

<a style="color:red"><strong>`git commit --amend`</strong></a><br>

- 커밋 메세지만 수정
  - 마지막으로 커밋하고 나서 수정한 것이 없을 때
- 이전 커밋 덮어쓰기
  - Staging Area에 새로 올라온 내용이 있을 때 ( git add )
