---
title: GIT Basic
date: 2023-11-15T15:15:58+09:00
description: GIT Basic
tags: ["git"]
type: post
showTableOfContents: true
---

# 전역 설정 (config --global)
> ``` Bash
> git config --global user.name "LeeSiny"
> git config --global user.email sinyoung.siny@gmail.com
> git config --global init.defaultBranch main
> ```  

<br/>
<br/>

# 깃 초기화 (init)
> ``` Bash
> git init
> ```  
  
<br/>  
<br/>
  
# 원격저장소를 로컬에 연결 (Remote, Clone)
> ### Remote
> : 원격 저장소를 가리키는 것, 프로젝트의 로컬 저장소에서 원격 저장소를 참조하는데 사용  
> \+ 원격저장소 default 별명 = origin
> ``` Bash
> git remote add origin <원격 저장소 주소>
> ```  

> ### Clone
> : 원격 저장소의 복제본을 만드는 것, 새로운 디렉터리에 원격 저장소의 모든 데이터를 가져와서 로컬에서 작업하는데 사용  
> \+ 일반적으로 "origin"이라는 이름의 리모트가 자동으로 설정
> ``` Bash
> git clone <원격 저장소 URL>
> ```

> ### 연결된 저장소 확인
> ``` Bash
> git remote -v
> ```  
> <br/>
> 
> 연결된 저장소 별명 변경 방법
> ``` Bash
> git remote rename <현재이름> <새로운이름>
> ```  
<br/>  
<br/>


# 변경 사항 확인 (Status, Log)
> ### Status
> : 아직 커밋되지 않은 변경 사항 확인  
> : 작업 디렉토리의 변경 상태, 스테이징 영역에 있는 변경 사항, 그리고 최근 커밋과 비교하여 어떤 파일이 수정되었는지 등을 보여줌
> ``` Bash
> git status
> ```

> ### Log
> : 커밋된 이력 확인  
> : 커밋 메시지, 저자, 날짜, 커밋 해시 등의 정보를 보여줌
> ``` Bash
> git log
> ```

<br/> 
<br/>


# Staging (Add)
: 변경된 파일을 스테이징 영역(Staging Area)에 추가하여 이를 다음 커밋에 포함시키는 데 사용

>### 모든 파일 스테이징
> #### 현재 디렉토리와 하위 디렉토리에 있는 모든 변경된 파일을 스테이징
> ``` Bash
> git add .
> ```
> 
> #### 현재 디렉토리와 모든 하위 디렉토리의 변경된 파일을 스테이징 (삭제된 파일도 스테이징)
> ``` Bash
> git add -A
> git add --all
> ```

>### 특정 파일 / 디렉토리 스테이징
> ``` Bash
> git add <파일명 / 디렉토리 경로>
> git add <파일명1> <파일명2> ... <파일명n>
> git add <디렉토리 경로1> <디렉토리 경로2> ... <디렉토리 경로n> 
> ```

<br/> 


# Staging Cancel (Restore, Reset)
: 스테이징 영역에 올라간 파일을 취소하거나 스테이징 영역 자체를 초기화하는 데 사용

> ### 모든 파일 스테이징 취소
> ``` Bash
> git restore --staged .
> git reset HEAD .
> ```

> ### 특정 파일 스테이징 취소
> ``` Bash
> git restore --staged <파일명>
> git reset HEAD <파일명>
> git restore --staged <파일명1> <파일명2> ... <파일명n> 
> git reset HEAD <파일명1> <파일명2> ... <파일명n> 
> ```

> ### 스테이징 영역 초기화
> ``` Bash
> git reset
> ``` 

<br/>
<br/>


# Commit
: 변경 사항을 저장하고 기록  
: 각 커밋은 프로젝트의 특정 시점에서의 상태를 나타내며, 커밋을 통해 소스 코드의 버전이 기록됨

> ### 커밋 생성
> : 스테이징 영역에 있는 변경 사항을 커밋으로 확정하고, 메시지를 함께 기록
> ``` Bash
> git commit -m "커밋 메시지"
> ```

<br/>
<br/>

# Push
### push
> ``` Bash
> git push <원격 저장소 별명> <로컬 브랜치 이름>
> ``` 

### 강제 push
> ``` Bash
> git push -f origin main
> git push -force origin main
> ``` 

<br/>
<br/>

