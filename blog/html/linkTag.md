---
title: HTML Link Tag
date: 2023-11-14T15:26:24+09:00 
description: 
tags: ["html"]
type: post
showTableOfContents: true
---

# 링크 (Link)
### \<a>
: 다른 페이지나 다른 사이트로 연결되는 하이퍼 링크 테그  
\+ \<a> 태그의 href속성(URL주소)을 명시

``` HTML
<a href="연결할 페이지나 사이트의 URL 주소"> 컨텐츠 </a>
```

## 링크 태그 속성

### href
vlaue => 이동하고자 하는 페이지/사이트/파일의 경로 

### target
: 링크로 연결된 문서를 어디에서 열지를 명시  
|     target value     |  설명  |
|--------------------|----------------------------------------|
|_blank| 새 창 or 새 탭|
|_self| 현재 프레임에서 오픈(기본설정)|
|_parent| 현재 화면을 불러온 부모의 프레임에서 오픈|
|_top| 현재창의 가장 최상위 프레임에서 오픈|
|프레임 이름| 지정된 프레임에서 오픈|

<br/>

### title
: 링크의 툴팁을 표시 (마우스 호버시 설명이 나옴)

>참고문헌  
><https://www.tcpschool.com/html/html_basic_links>