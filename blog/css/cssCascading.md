---
title: "CSS 개념, 적용 방법, 캐스케이딩"
date: 2023-11-15T10:05:13+09:00
description: "CSS 개념, 적용 방법, 캐스케이딩(우선순위)"
tags: ["CSS"]
type: post
showTableOfContents: true
---

# CSS 란?
CSS (Cascading Style Sheet)  
: HTML과 함께 웹을 구성하는 기본 프로그래밍 요소  
=> 색상이나 크기, 이미지 크기나 위치, 배치 방법 등 웹 문서의 디자인 적인 요소를 담당  
\+ HTML로 부터 디자인적인 요소를 분리해 정의 할 수 있음
\+ 자바스크립트와 연계해 동적인 콘텐츠 표현 / 디자인 적용 가능
### CSS 구성
```
   선택자   {속성:값; 속성:값;...}  
 --선택자--|------- 선언부 -------
```  
<br/>

## CSS 적용 방법 
### 인라인 스타일
: HTML 요소 내부에 style 속성을 사용하여 CSS 스타일을 적용하는 방법  
\- HTML 태그에 필요한 디자인을 바로 적용할 수 있지만 일관된 디자인 체계를 유지하는데 방해가 됨
``` HTML
<body>
  <h1 style="color:blue; padding-left:50px;">
    인라인 스타일 이용
  </h1>
</body>
```  
<br/>

### 내부 스타일 시트
: HTML 문서 \<head>태그 내에 \<style>태그를 사용하여 CSS 스타일을 적용하는 방법  
\- 내부 스타일 시트는 해당 HTML 문서에만 스타일을 적용할 수 있어  css의 재활용이 안됨
``` HTML
<head>
  <style>
    body {
      background-color: green;
    }
    h1 {
      color: blue;
      padding-left: 50px;
    }
  </style>
</head>
```  
<br/>  

### 외부 스타일 시트
: 별도의 파일에 CSS문서를 작성하고 해당 CSS를 필요로 하는 HTML 문서 \<head>태그 내에 \<link>태그를 사용하여 CSS 스타일을 적용하는 방법  
``` HTML
<head>
  <link rel="stylesheet" type="text/css" href="simple.css">
  <link rel="stylesheet" type="text/css" href="https://cdn.simplecss.org/simple.css">
</head>
```  
<br/>  

## CSS 캐스케이딩 (Cascading)
: CSS 적용 우선 순위  
> 중요도 : CSS 선언 위치에 따라 우선순위가 달라짐  
> 명시도 : 선택자가 지정하는 대상이 명확할수록 우선순위가 높아짐  
> 코드 순서: 나중에 선언된 스타일(코드)가 우선순위가 높음 

### 우선 순위
> 0\. 사용자 !important 스타일 (색약자, 저시력자 등을 위해서 특별히 설정된 스타일)  
> 1\. 제작자 !important 스타일   
> 2\. 제작자 스타일  
> 3\. 사용자 스타일  
> 4\. 브라우저(사용자 에이전트) 스타일
<br/>

### 중요도 
> 제작자 스타일 내  
> 1\. 인라인 스타일  
> 2\. 내부 스타일 시트  
> 3\. 외부 스타일 시트  
> 4\. 브라우저 디폴트 스타일  

### 명시도
> 0\. !important   
> 1\. 인라인 스타일 속성  
> 2\. 아이디 선택자  
> 3\. 클래스 선택자  
> 3\. 속성 기반 선택자  
> 3\. 가상 클래스 선택자  
> 3\. 가상 요소 선택자  
> 4\. 태그 선택자  
> 5\. 전체 선택자  
> 6\. 상위요소에 상속된 속성  

### 코드 순서
> ``` CSS
>p { color: green; } 
>p { color: blue; } /* 우선 적용 */
>
>.blue { color: blue; }
>.green { color: green; } /* 우선 적용 */
>
> /* 코드 순서만 놓고 본 결과 = p태그의 색상은 green */
>```

<br/>
<br/>  

<hr/>  

>참고문헌  
><https://www.tcpschool.com/css/intro>
><http://www.devdic.com/css/reference/documents/document:1806/%EC%84%A0%ED%83%9D%EC%9E%90(Selector)%EC%9D%98-%EC%9A%B0%EC%84%A0-%EC%88%9C%EC%9C%84>