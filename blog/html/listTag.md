---
title: HTML List Tag
date: 2023-11-13T15:43:39+09:00 
description: 
tags: ["html"]
type: post
showTableOfContents: true
---

# 리스트 (List)
### \<li>
: \<ul>과 \<ol>안에서 각 항목을 나열할 때 사용  
\+ 블록 요소

<br/>

### \<ul>
: 순서가 없는 리스트(Unordered List)
\+ 블록 요소
``` HTML
<ul>
  <li>강아지</li>
  <li>고양이</li>
  <li>호랑이</li>
</ul>
```
<ul>
  <li>강아지</li>
  <li>고양이</li>
  <li>호랑이</li>
</ul>

<br/> 

### \<ol>
: 순서가 있는 리스트(Ordered List)
\+ 블록 요소
\+ type, start, reversed 같은 속성이 있음
``` HTML
<ol>
  <li>강아지</li>
  <li>고양이</li>
  <li>호랑이</li>
</ol>
```
<ol>
  <li>강아지</li>
  <li>고양이</li>
  <li>호랑이</li>
</ol>

<br/>

### \<dl>
: 정의 리스트(Description List)  
\+ 블록 요소  
\+ \<dt> : 용어의 이름  
\+ \<dd> : 해당 용어에 대한 정의  

``` HTML
<dl>
  <dt>강아지</dt>
  <dd>- 귀여워</dd>
  <dt>고양이</dt>
  <dd>- 더 귀여워</dd>
</dl>
```
<dl>
  <dt>강아지</dt>
  <dd>- 귀여워</dd>
  <dt>고양이</dt>
  <dd>- 더 귀여워</dd>
</dl>

<br/>
<br/> 

<hr/>  

>참고문헌  
>https://www.tcpschool.com/html/html_basic_lists