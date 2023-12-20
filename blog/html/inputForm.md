---
title: HTML 입력 양식
date: 2023-11-14T16:50:24+09:00
description: HTML 입력 양식 (form, input ...)
tags: ["html"]
type: post
showTableOfContents: true
---

# 폼(Form) 양식
: 사용자와 웹사이트 또는 어플리케이션이 서로 상호 작용하기 위해 사용  
=> 사용자로부터 입력을 받거나, 사용자가 입력한 데이터를 서버에 보낼때 사용
  
<br/>

## \<form>
: 입력 양식 전체를 감싸는 태그
|     form value     |  설명  |
|--------------------|----------------------------------------|
|method| 전송 방식 선택 (GET / POST)|
|name| form의 이름|
|action| form을 통해 작성된 데이터를 보낼 주소|

> GET : URL에 데이터가 표시됨 => 보안에 취약  
> POST : URL에 데이터가 표시되지 않음

<br/> 

## \<input>
: 사용자로 부터 데이터를 입력 받기 위해 사용
|     input attribute     |  설명  |
|--------------------|----------------------------------------|
|type| input 태그의 타입 지정|
|required| 필수 입력 지정|
|maxLength| 최대 입력 문자 개수 지정|
|placeholder| 힌트 표시(클릭시 내용 사라짐)|
|readonly| 읽기 전용(사용자 지정 불가)|
|autofocus| 마우스 커서 자동 포커스|
|autocomplete| 자동완성 설정|

<br/>

|     input type value     |  설명  |
|--------------------|----------------------------------------|
|text| 텍스트 입력 필드 (텍스트는 한 줄 까지)|
|password| 필수 입력 지정|
|radio| 라디오 버튼 (1개만 선택 가능)|
|checkbox| 체크박스 (2개이상 선택 가능)|
|file| 파일 첨부 가능|
|submit| form 전송|
|reset| form 리셋|

<br/> 

## \<textarea> 
: 문장 입력 => 여러 줄의 긴 내용 입력 가능
``` HTML
<textarea>

  여기에 적으세요.

</textarea>
``` 
<br/> 

## \<select>, \<option>
: 드롭 다운 메뉴에서 선택 가능한 양식  
\+ selected : 기본 선택 값
``` HTML
<select name="animal">
  <option value="panda"> 판다
  <option value="cat" selected> 고양이
  <option value="dog"> 강아지
  <option value="tiger"> 호랑이
</select>
``` 

<br/> 

## \<fieldset>
: form 요소와 관련된 입력 양식, 데이터 들을 그룹화할 때 사용
\+ \<legend> : fieldset의 제목을 정의
``` HTML
<form>
  <fieldset>
    <legend>Login</legend>
    E-mail : <br>
    <input type="e-mail"><br>
    Password : <br>
    <input type="text" name="email"><br><br>
    <input type="submit" value="submit">
  </fieldset>
</form>
``` 

<br/>
<br/>  

<hr/>  

>참고문헌  
><https://www.tcpschool.com/html/html_input_forms>