---
title: "CSS 선택자"
date: 2023-11-15T15:15:58+09:00
description: "CSS 선택자"
tags: ["CSS"]
type: post
showTableOfContents: true
---

# 선택자 란?
선택자 (Selector)  
: 스타일을 적용할 HTML요소를 선택하기 위해서 선택자를 사용
<br/>

> ### 전체 선택자
> : 요소 내부의 모든 요소를 선택
> ``` CSS
> * { color: teal; text-decoration: underline; }
> h1 * { color: teal; text-decoration: underline; }
> ```

> ### HTML 요소 선택자
> : HTML 요소의 이름을 직접 사용하여 선택
> ``` HTML
> <h2>이 부분에 스타일을 적용합니다.</h2>
> ```
> ``` CSS
> h2 { color: teal; text-decoration: underline; }
> ```

> ### 아이디(id) 선택자
> : CSS를 적용할 대상으로 특정 요소를 선택할 때 사용
> ``` HTML
> <h2 id="heading">이 부분에 스타일을 적용합니다.</h2>
> ```
> ``` CSS
> #heading { color: teal; text-decoration: line-through; }
> ```

> ### 클래스(class) 선택자
> : 특정 집단의 여러 요소를 한 번에 선택할 때 사용
> ``` HTML
> <h2 class="headings">이 부분에 스타일을 적용합니다.</h2>
> <p>이 부분은 선택되지 않음</p>
> <h3 class="headings">이 부분에도 같은 스타일을 적용합니다.</h3>
> ```
> ``` CSS
> .headings { color: deepskyblue; text-decoration: overline; }
> ```

> ### 그룹 선택자
> : 여러 선택자를 같이 사용하고자 할 때 사용
> ``` CSS
> h1 { color: navy; }
> h1, h2 { text-align: center; }
> h1, h2, p { background-color: lightgray; }
> ```

> ### 속성 선택자
> : 여러 선택자를 같이 사용하고자 할 때 사용  
> <br/>  
>  
> #### 기본 속성 선택자
> ``` CSS
> /* [속성이름] 선택자 */
> [title] { background: black; color: yellow; }
>
> /* [속성이름="속성값"] 선택자 */
> [title="first h2"] { background: black; color: yellow; }
>
> /* A[속성이름] 선택자 */
> div[title] { background: black; color: yellow; }
> ```
> <br/>  
> 
> #### 문자열 속성 선택자
> ``` CSS
> /* [속성이름~="속성값"] 선택자 */
> /* 특정 속성의 속성값에 특정 문자열로 이루어진 하나의 단어를 포함하는 요소를 모두 선택 */
> [title~="first"] { background: black; color: yellow; }
>
> /* [속성이름|="속성값"] 선택자 */
> /* 특정 속성의 속성값이 특정 문자열로 이루어진 하나의 단어로 시작하는 요소를 모두 선택 */
> [title|="first"] { background: black; color: yellow; }
>
> /* [속성이름^="속성값"] 선택자 */
> /* 특정 속성의 속성값이 특정 문자열로 시작하는 요소를 모두 선택 */
> [title^="first"] { background: black; color: yellow; }
>
> /* [속성이름$="속성값"] 선택자 */
> /* 특정 속성의 속성값이 특정 문자열로 끝나는 요소를 모두 선택 */
> [title$="first"] { background: black; color: yellow; }
>
> /* [속성이름*="속성값"] 선택자 */
> /* 특정 속성의 속성값에 특정 문자열를 포함하는 요소를 모두 선택 */
> [title*="first"] { background: black; color: yellow; }
> ```

<br/>


# 기본 선택자

## 결합 선택자
: 결합 선택자는 연관된 선택자들 간의 관계를 설정함

> ### 일치 선택자
> : A와 B를 동시에 만족하는 요소 선택
> ``` CSS
> AB { background: black; color: yellow; }
> ``` 

> ### 자손 선택자
> : A의 모든 자손(자식, 손자, ...) 요소 중 선택
> ``` CSS
> /* A 밑에 있는 모든 B선택 */
> A B { background: black; color: yellow; }
> ``` 

> ### 자식 선택자
> : A의 바로 밑 자식 요소 선택
> ``` CSS
> /* A 바로 밑에 있는 B선택 */
> A>B { background: black; color: yellow; }
> ``` 

<br/>


## 동위 선택자
: 동위 관계에 있는 요소 중에서 해당 요소보다 뒤에 존재하는 특정 타입의 요소를 모두 선택  
\+ 동위 관계 : HTML 요소의 계층 구조에서 같은 부모 요소를 가지고 있는 요소

> ### 일반 동위 선택자 (= 일반 형제 선택자)
> : A의 모든 형제 요소 선택
> ``` CSS
> A~B { background: black; color: yellow; }
> ```  

> ### 인접 동위 선택자 (= 인접 형제 선택자)
> : A의 다음 형제 하나만 선택
> ``` CSS
> /* A 의 형제 중 바로 다음에 오는 B형제 한개만 선택*/
> A+B { background: black; color: yellow; }
> ```   
  
<br/>  
<br/>  

# 의사(가상) 선택자
: HTML요소를 직접적으로 선택하지 않고, 해당 요소의 상태(state)에 따라 선택

## 의사 요소
: 해당 HTML 요소의 특정 부분만을 선택할 때 사용  
\+ 하나의 HTML 요소에 여러 개의 의사 요소 동시 적용 가능
``` CSS
 선택자::의사요소이름 {속성: 속성값;}
```

> |의사 요소 선택자   |설명                           |
> |-----------------|-------------------------------|
> |::first-letter|텍스트의 첫 글자만을 선택(단, 블록 타입 요소에만 사용할 수 있음)|
> |::first-line|텍스트의 첫 라인만을 선택(단, 블록 타입 요소에만 사용할 수 있음)|
> |::before|특정 요소의 컨텐츠 바로 앞에 다른 요소를 삽입할 때 사용|
> |::after|특정 요소의 컨텐츠 바로 뒤에 다른 요소를 삽입할 때 사용|
> |::selection|해당 요소에서 사용자가 선택한 부분만을 선택할 때 사용|

<br/>

## 의사 클래스
: HTML 요소의 특별한 '상태(state)'를 명시할 때 사용  
``` CSS
 선택자:의사클래스이름 {속성: 속성값;} 

 선택자.클래스이름:의사클래스이름 {속성: 속성값;} 
 선택자#아이디이름:의사클래스이름 {속성: 속성값;}
```

> ### 동적 의사 클래스
> |선택자   |설명                           |
> |-----------------|-------------------------------|
> |:link|사용자가 아직 한 번도 해당 링크를 통해서 연결된 페이지를 방문하지 않은 상태(기본 상태)|
> |:visited|사용자가 한 번이라도 해당 링크를 통해서 연결된 페이지를 방문한 상태|
> |:hover|사용자의 마우스 커서가 링크 위에 올라가 있는 상태|
> |:active|사용자가 마우스로 링크를 클릭하고 있는 상태|
> |:focus|초점이 맞춰진 상태|

> ### 상태 의사 클래스
> |선택자   |설명                           |
> |-----------------|-------------------------------|
> |:checked|체크된 상태의 input 요소를 모두 선택|
> |:enabled|사용할 수 있는 input 요소를 모두 선택|
> |:disabled|사용할 수 없는 input 요소를 모두 선택|> 

> ### 정합성 체크 선택자
> |선택자   |설명                           |
> |-----------------|-------------------------------|
> |:valid|정합성 검증이 성공한 input/form 요소를 선택|
> |:invalid|정합성 검증이 실패한 input/form 요소를 선택|

> ### 구조 의사 클래스
> |선택자   |설명                           |
> |-----------------|-------------------------------|
> |:first-child|모든 자식 요소 중에서 첫 번째에 위치하는 자식(child) 요소를 모두 선택|
> |:last-child|모든 자식 요소 중에서 마지막에 위치하는 자식 요소를 모두 선택|
> |:nth-child|모든 자식 요소 중에서 앞에서부터 n번째에 위치하는 자식 요소를 모두 선택|
> |:nth-last-child|모든 자식 요소 중에서 뒤에서부터 n번째에 위치하는 자식 요소를 모두 선택|
> |:first-of-type|모든 자식 요소 중에서 첫 번째로 등장하는 특정 요소를 모두 선택|
> |:last-of-type|모든 자식 요소 중에서 마지막으로 등장하는 특정 요소를 모두 선택|
> |:nth-of-type|모든 자식 요소 중에서 n번째로 등장하는 특정 요소를 모두 선택|
> |:nth-last-of-type|모든 자식 요소 중에서 뒤에서부터 n번째로 등장하는 특정 요소를 모두 선택|
> |:only-child|자식 요소를 단 하나만 가지는 모든 요소의 자식 요소를 선택|
> |:only-of-type|자식 요소를 특정 요소 단 하나만 가지는 모든 요소의 자식 요소를 선택|
> |:empty|아무런 자식 요소도 가지지 않는 요소를 모두 선택|
> |:root|문서의 root 요소를 선택|

> ### 기타 의사 클래스
> |선택자   |설명                           |
> |-----------------|-------------------------------|
> |:not|모든 선택자와 함께 사용할 수 있으며, 해당 선택자를 반대로 적용|
> |:lang|특정 요소를 언어 설정에 따라 다르게 표현할 때에 사용|

<br/>
<br/>  

<hr/>  

>참고문헌  
><https://www.tcpschool.com/css/intro>
><http://www.devdic.com/css/reference/documents/document:1806/%EC%84%A0%ED%83%9D%EC%9E%90(Selector)%EC%9D%98-%EC%9A%B0%EC%84%A0-%EC%88%9C%EC%9C%84>