---
title: GIT Branch
date: 2023-11-16T12:47:24+09:00
description: GIT Branch
tags: ["git"]
type: post
showTableOfContents: true
---
# Branch
: 프로젝트의 특정 작업을 독립적으로 개발하고 관리할 수 있게 해줌  
\+ 각각의 브랜치는 프로젝트의 특정 상태를 나타내며, 변경 사항을 안전하게 실험하고 적용할 수 있는 환경을 제공해줌  
\+ 여러 작업을 병렬로 진행하거나 특정 기능 또는 버그 수정을 독립적으로 개발할 수 있음  

<br/>

## Branch 조회
> ### 현재 저장소의 모든 브랜치 목록 확인
> ``` Bash
> git branch
> ```

> ### 로컬 및 원격 저장소의 모든 브랜치 목록 확인
> ``` Bash
> git branch -a
> ```

> ### 브랜치 해시 확인 방법
> ``` Bash
> git log --oneline --decorate
> ```

> ### 브랜치 분기, 히스토리 확인 방법
> ``` Bash
> git log --oneline --decorate --graph --all
> ```


<br/>

## Branch 생성
> ### 새로운 브랜치 생성
> ``` Bash
> git branch <브랜치 이름>
> ```

> ### 새로운 브랜치 생성 (현재 HEAD가 아닌 다른 지점에서 브랜치 생성)
> ``` Bash
> git branch <브랜치 이름> <브랜치 해시>
> ```

> ### 브랜치 생성 및 해당 브랜치로 전환
> ``` Bash
> git checkout -b <브랜치 이름>
> git switch -c <브랜치 이름>
> ```


<br/>

## Branch 전환
> ### <브랜치 이름>으로 브랜치 전환
> ``` Bash
> git checkout <브랜치 이름>
> git switch -c <브랜치 이름>
> ```


<br/>

## Branch 삭제
> ### 브랜치 삭제 (병합된 브랜치만 삭제 가능)
> ``` Bash
> git branch -d <브랜치 이름>
> ```

> ### 강제로 브랜치 삭제
> ``` Bash
> git branch -D <브랜치 이름>
> ```


<br/>

## Branch 병합
> ### 현재 본인이 있는 브랜치에 다른 브랜치를 병합
> ``` Bash
> git merge <병합할 브랜치 이름>
> ```

<br/>
<br/>