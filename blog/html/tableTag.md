---
title: HTML Table Tag
date: 2023-11-14T16:20:00+09:00 
description: 
tags: ["html"]
type: post
showTableOfContents: true
---

# 테이블 (Table)
### \<table>
: 여러 종류의 데이터를 보기 좋게 정리하여 보여주는 표 
\+ 블록 요소

#### \<caption> : 테이블의 제목
#### \<tr> : 테이블의 행
#### \<th> : 제목 셀 
#### \<td> : 일반 셀  

``` HTML
<table>
  <caption>동물계</caption>
  <tr>
    <th>어류</th>
    <th>포유류</th>      
  </tr>
  <tr>
    <td>참치</td>
    <td>강아지</td>
  </tr>
  <tr>
    <td>고등어</td>
    <td>고양이</td>
  </tr>
</table>
```
<table>
  <caption>동물계</caption>
  <tr>
    <th>어류</th>
    <th>포유류</th>      
  </tr>
  <tr>
    <td>참치</td>
    <td>강아지</td>
  </tr>
  <tr>
    <td>고등어</td>
    <td>고양이</td>
  </tr>
</table>

<br/> 

## 테이블 태그 속성

### colspan
: 테이블의 열을 합침 

### rowspan
: 테이블의 행을 합침

<br/> 
<br/> 

<hr/>  

>참고문헌  
><https://www.tcpschool.com/html/html_basic_tables>