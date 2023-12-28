---
title: "명령어(Command)"
meta_title: "명령어(Command)"
description: "소스 코드와 명령어, 명령어의 구조"
date: 2023-12-15T10:59:28+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **소스코드와 명령어**
프로그래밍 언어로 만든 소스 코드들이 실행되려면 컴퓨터 내부에서 이해할 수 있는 명령어로 변환이 되야함  

<br>

## **고급언어와 저급언어**  
| 구분 | 고급 언어 | 저급 언어 |
|------|-----------|-----------|
|호환성| 좋음 | 나쁨 |
|용이성| 쉬움 | 어려움 |
|실행속도| 상대적으로 느림 | 빠름 | 

### **고급 언어(High-Level Programming Language)**
프로그래밍 언어와 같이 사람이 이해하기 쉽게 만들어진 언어  
=> C, C++, Java, Python 등  

<br>

#### **고급언어의 필요성**
사람이 읽고 쓰기 편함  
가독성이 좋음  
변수나 함수 등 문법을 이용해 복잡한 프로그램을 구현할 수 있음  
 
<br>
<hr>

### **저급 언어(Low-Level Programming Language)**
컴퓨터가 이해하고 실행하는 있는 언어

=> 명령어 : 기계어, 어센블리어
 
<br>

#### **기계어(Machine Language)**
0과 1의 명령어 비트로 이루어진 언어
(이진수로 나열 시 너무 길어지기 때문에 가독성을 위해 십육진수로 나타내기도 함)

{{< notice "note" >}}  
전문적인 지식이 없으면 프로그램 작성 및 이해가 어려움  
기종마다 기계어가 다르므로 언어의 호환성이 없음  
프로그램 유지보수가 어려움  
{{< /notice >}}

<br>

#### **어셈블리어(Assembly Language)**
기계어를 사람이 어느정도 이해할 수 있는 형태로 번역한 언어
(기계어와 1:1로 대응되는 기호로 이루어진 언어)
=> 기호 코드(Mnemonic Code)라고도 함

{{< notice "note" >}}  
기계어와 가장 유사하며, 기계어로 번역하기 위해서는 어셈블러(Assembler)가 필요
{{< /notice >}}

<br>

#### **저급언어의 필요성**
하드웨어와 밀접한 임베디드 개발자, 게임 개발자, 정보 보안 분야 등은 저급언어(어셈블리어)를 이용할 일이 많음  
언어의 "작성" 뿐만 아니라 "관찰"의 시점에서 중요  
어셈블리어를 읽으면서 컴퓨터 프로그램 실행 과정을 파악하고, 각 절차를 추적하고 관찰할 수 있음  
 
<br>
<hr>
 
## **컴파일, 인터프리터**
고급 언어를 저급언어로 변환하는 방식

<br>

### **컴파일 언어**
컴파일러에 의해 소스 코드 전체가 저급 언어로 변환 후 프로그램이 실행되는 고급 언어  
=> C  

```
고급 언어 => 컴파일 => 저급언어
소스 코드   컴파일러   목적 코드
```

<br>

#### **컴파일(Compile)**
컴파일 언어로 작성된 소스 코드 전체가 저급 언어로 변환되는 과정
 
<br>

#### **컴파일러(Compiler)**
컴파일을 수행해주는 도구로 전체 소스 코드를 저급 언어로 컴파일  

{{< notice "note" >}}  
개발자가 작성한 소스코드 전체를 쭉 훑어보며 소스 코드에 문법적인 오류는 없는지, 실행 가능한 코드인지, 실행하는 데 불필요한 코드는 없는지 등을 따짐

=> 이때, 컴파일러가 소스 코드 내에서 오류를 하나라도 발견하면 해당 소스코드는 컴파일에 실패함
{{< /notice >}}

<br>

#### **목적 코드(Object Code)**
컴파일러를 통해 저급 언어로 변환된 코드
 
<br>
<hr>

### **인터프리터 언어**
인터프리터에 의해 소스 코드가 한 줄씩 실행되는 고급 언어
=> Python

{{< notice "note" >}}  
코드를 한줄씩 차례대로 실행  
소스코드를 저급언어로 변환하는 시간을 기다리지 않고 바로 실행 가능  
소스 코드 내 N번째 줄에 오류가 있더라도 N-1번째 줄까지는 정상적으로 실행이 가능  
{{< /notice >}}  
 
<br>

### **인터프리터(Interpreter)**
소스코드를 한줄씩 저급 언어로 변환해 실행해주는 도구
 
<br>
<hr>

### **컴파일 언어와 인터프리터 언어**
인터프리터 언어는 일반적으로 컴파일 언어보다 느림
=> 컴파일 언어는 소스코드 전체를 저급언어로 변환한 후 실행
=> 인터프리터 언어는 소스 코드 줄마다 저급언어로 변환하여 실행 (상대적으로 느림)

{{< notice "note" >}}  
컴파일 언어와 인터프리터 언어를 명확히 구분하는 것이 어려움
=> 여러 프로그래밍 언어들이 두가지 방식을 혼용해 사용하기 때문
{{< /notice >}}  

<br>
<hr>

## **목적 파일 vs 실행 파일**
### **목적 파일**
목적 코드로 이루어진 파일

{{< notice "note" >}}  
C에서는 *.o 형태의 확장자를 가짐  
*.o는 소스 파일(*.c) 내용을 저급 언어로 변환한 파일일 뿐 실행할 수는 없음  
(실행을 위해서는 링킹 작업이 필요)  

**링킹** : 목적 코드가 실행 파일이 되기 위해 거치는 작업  
=> 목적 파일에는 없는 외부 기능들을 연결하는 작업  
=> 링킹 작업이 완료되면 하나의 실행 파일이 생성  
{{< /notice >}}  

<br>

### **실행 파일**
코드를 실행하는 파일

{{< notice "note" >}}  
**실행 파일 생성 과정** 
소스 파일(*.c) -> 컴파일 -> 목적 파일(*.o) -> 링킹 -> 실행 파일
{{< /notice >}}  

<br>
<hr>

# **명령어의 구조**
명령어 = 기계어나 어셈블리어를 이루는 하나하나  
=> 무엇을 대상으로, 무엇을 수행하라  
=> 어떤 '작업'을 '무엇'이 수행해라는 구조로 되어 있음  

<br>

## **연산코드와 오퍼랜드**

### **명령어(Command)** 
연산 코드 + 오퍼랜드

<br>

### **연산코드(Operation Code)**
명령어가 수행할 연산 (= 연산자)

{{< notice "info" >}}  
4가지 종류 (연산코드의 종류, 생김새는 CPU마다 다름)

1. 데이터 전송  
2. 산술/논리 연산  
3. 제어 흐름 변경    
4. 입출력 제어  

{{< /notice >}}  

<br>
<hr>

### **오퍼랜드(Operand)**
연산에 사용할 데이터 또는 연산에 사용할 데이터가 저장된 위치 (= 피연산자)  

오퍼랜드의 필드 = 주소 필드  
=> 오퍼랜드는 없거나 하나 이상일 수도 있음  

숫자와 문자 등 데이터를 직접 명시하거나 메모리나 레지스터 주소 등 간접 명시  
=> 대부분은 연산에 사용할 데이터의 위치(메모리 주소 또는 레지스터 이름)가 입력됨  

<br>

#### **오퍼랜드의 개수**
오퍼랜드가 없는 명령어 = 0-주소 명령어 => (연산코드)  
오퍼랜드가 한개인 명령어 = 1-주소 명령어 => (연산코드 + 오퍼랜드)  
오퍼랜드가 두개인 명령어 = 2-주소 명령어 => (연산코드 + 오퍼랜드 + 오퍼랜드)  
오퍼랜드가 세개인 명령어 = 3-주소 명령어 => (연산코드 + 오퍼랜드 + 오퍼랜드 + 오퍼랜드)  

<br>
<hr>

## 오퍼랜드의 주소 지정 방식

### **오퍼랜드에 데이터를 간접 명시(주소) 하는 이유**
명령어의 길이가 제한되어있어 간접 명시하는 경우가 많음

{{< notice "note" >}}  
하나의 명령어의 크기 N비트, 연산 코드 필드 M비트 => N - M 비트  
오퍼랜드 2개일 때, 2-주소 명령어에서 표현할 수 있는 데이터의 크기 = 2^6비트 (64비트)  
오퍼랜드 3개일 때, 3-주소 명령어에서 표현할 수 있는 데이터의 크기 = 2^4비트 (16비트)  

**데이터가 아니라 데이터가 저장된 주소를 저장**  
=> 메모리 주소 또는 레지스터에 저장할 수 있는 공간만큼 커지게 됨  
{{< /notice >}}  

<br>
<hr>

### **유효 주소(Effective Address)**
연산의 대상이 되는 데이터가 저장된 위치

<br>
<hr>

### **주소 지정 방식(Addressing Mode)**
연산에 사용할 데이터 위치를 찾는 방법 (= 유효 주소를 찾는 방법)
=> 현대 CPU는 다양한 주소 지정 방식을 사용

<br>

#### **즉시 주소 지정 방식(Immediate Addressing Mode)**
**데이터를 직접 명시**  
연산에 사용할 데이터를 오퍼랜드 필드에 직접 명시하는 방식  
=> 가장 간단한 형태의 주소 지정 방식  

=> 연산 코드 + 연산에 사용할 데이터 형태  

**장점**  
연산에 사용할 데이터를 직접 명시하기 때문에 아래 주소 지정 방식들보다 속도가 빠름 

**단점**  
표현할 수 있는 데이터의 크기가 작아짐  

<br>
<hr>

#### **직접 주소 지정 방식(Direct Addressing Mode)**
**메모리에 데이터를 명시하고 메모리 주소를 참조**  
오퍼랜드 필드에 유효 주소를 직접 명시하는 방식  

=> 연산 코드 + 유효 주소 형태  
(연산에 사용할 데이터는 메모리 내에) 

**장점**  
표현할 수 있는 데이터의 크기가 즉시 주소 지정 방식에 비해 큼  

**단점**  
표현할 수 있는 유효 주소 수가 여전히 제한적임  

<br>
<hr>

#### **간접 주소 지정 방식(Indirect Addressing Mode)**
**메모리에 데이터를 명시하고 메모리 주소를 참조**  
유효주소의 주소를 오퍼랜드 필드에 명시하는 방식  

=> 연산 코드 + 유효 주소의 주소 형태  
(연산에 사용할 데이터, 유효 주소는 메모리 내에)

**장점**  
직접 주소 지정 방식보다 표현할 수 있는 유효 주소의 범위가 넓어짐  

**단점**  
데이터를 찾기 위해 메모리 접근을 두번하게 되면서 앞선 방법들보다 속도가 느려짐  

<br>
<hr>

#### **레지스터 주소 지정 방식(Register Addressing Mode)**  
**레지스터에 데이터를 명시하고 레지스터 주소를 참조**  
데이터를 저장한 레지스터를 오퍼랜드 필드에 직접 명시하는 방식  

=> 연산 코드 + 유효 주소의 형태  
(연산에 사용할 데이터는 레지스터 내에)

**장점**  
직접 주소 지정 방식보다 빠르게 데이터에 접근 가능  

**단점**  
표현할 수 있는 레지스터 크기에 제한이 생길 수 있음  
 
<br>
<hr>

#### **레지스터 간접 주소 지정 방식(Register Indirect Addressing Mode)**
**레지스터에 데이터를 명시하고 레지스터 주소를 참조**  
연산에 사용할 데이터는 메모리에 저장하고, 그 주소를 저장한 레지스터를 오퍼랜드 필드에 명시하는 방법  

=> 연산 코드 + 유효 주소를 저장한 레지스터 형태   
(유효주소는 레지스터 내에, 연산에 사용할 데이터는 메모리 내에)

**장점**  
메모리에 접근하는 횟수가 한번으로 줄어들어 속도가 간접 주소 지정방식보다 빠름  

<br>
<hr>

## 스택과 큐
스택 = 후입선출 (LIFO)  
큐 = 선입선출 (FIFO)


<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)