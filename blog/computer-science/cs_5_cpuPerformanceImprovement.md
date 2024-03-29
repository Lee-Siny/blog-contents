---
title: "CPU의 성능 향상 기법"
meta_title: "CPU의 성능 향상 기법"
description: "클럭, 코어, 스레드, 명령어 병렬 처리 기법, ISA, CISC, RISC"
date: 2023-12-25T15:06:57+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **빠른 CPU를 위한 설계 기법**

## **클럭**
CPU를 빠르게 하기 위한 방법 1 => 클럭 속도를 높이는 방법

컴퓨터 부품들은 클럭 신호에 맞춰 움직이고, CPU는 명령어 사이클에 맞춰 명령어들을 실행  
=> 클럭 속도가 높아지면 CPU는 명령어 사이클을 더 빠르게 반복할 거고 다른 부품들도 더 빠르게 작동함  

{{< callout type="info" >}}  
클럭 속도의 단위는 헤르츠(Hz)  
헤르츠 = 1초에 클럭이 반복되는 횟수  

(클럭이 1초에 100번 반복되면 CPU의 클럭 속도는 100Hz)  
{{< /callout >}}  

{{< callout type="info" >}}  
클럭 속도는 일정하지 않음  

필요한 작업량에 따라서 유연하게 조절되며, 최대 클럭 속도를 강제로 끌어올리는 방법을 오버클럭킹(overclocking)이라고 함  
(CPU는 고성능을 요하는 순간에는 순간적으로 속도를 높이고, 그렇지 않을 때는 유연하게 클럭 속도를 낮춤)  

=> 클럭 속도를 너무 극단적으로 높이다보면 발열 문제 발생  
{{< /callout >}}  


<br>
<hr>

## **코어 (Core)**
CPU 내부에서 명령어를 실행하는 부품  
=> 기술 발전으로 현대 CPU에는 명령어를 실행하는 부품이 여러 개 존재할 수 있게 되었음  

{{< callout type="info" >}}  
CPU의 연산 속도가 무조건 코어 수에 비례하여 증가하지는 않음  
처리하고자 하는 작업량보다 너무 코어가 많아도 성능에는 크게 영향이 없음  

=> 코어마다의 처리해야 할 연산이 적절히 분배되는 것이 중요함  
{{< /callout >}}  

{{< callout type="info" >}}  
**멀티 코어 (= 멀티 코어 프로세서)**  
여러 개의 코어를 가지고 있는 것  

**싱글 코어 (= 싱글 코어 프로세서)**  
하나의 코어를 가지고 있는 것  
{{< /callout >}}  

<br>
<hr>

## **스레드 (Thread)**
실행 흐름의 단위

### **하드웨어적 스레드**  
하나의 코어가 동시에 처리하는 명령어 단위  

{{< callout type="info" >}}  
**1코어 1스레드 CPU**  
하나의 코어가 하나의 명령어를 처리하는 CPU   

**멀티스레드 프로세서/CPU (Multi-Thread Processor/CPU)**  
하나의 코어로 여러 명령어를 동시에 처리하는 CPU  
=> 멀티스레드 프로세서를 실제로 설계하는 일은 매우 복잡하지만, 가장 큰 핵심은 레지스터  

(하이퍼스레딩 : 인텔의 멀티스레드 기술)  
{{< /callout >}}  

### **소프트웨어적 스레드**  
하나의 프로그램에서 독립적으로 실행되는 단위  
(1코어 1스레드 CPU가 여러 스레드로 만들어진 프로그램을 실행할 수 있음)  

{{< callout type="info" >}}  
**멀티스레드 프로그래밍**  
하나의 프로그램을 여러 개의 스레드로 분할하여 동시에 실행하는 것  
{{< /callout >}}  

<br>
<hr>

# **명령어 병렬 처리 기법**  
**(ILP : Instruction-Level Parallelism)**  
명령어를 동시에 처리하여 CPU를 한시도 쉬지 않고 작동시키는 기법  
=> CPU를 빠르게 만드는 것도 중요하지만, CPU의 유휴 시간 (대기 시간)을 줄이고 최대한 효율적으로 작동할 수 있도록 하는 것도 중요  

## **명령어 파이프라인**  
**(Instruction Pipeline)**  
여러 명령어가 순차적으로 연결되어 하나의 프로세스로 실행되는 방식  
=> 하나의 명령어의 출력이 다음 명령어의 입력으로 연결되어 연속적으로 실행되는 구조  

{{< callout type="info" >}}  
**명령어 처리 과정**   
1. 명령어 인출 (Instruction Fetch)  
2. 명령어 해석 (Instruction Decode)  
3. 명령어 실행 (Execute Instruction)  
4. 메모리 접근 (Memory Access)  
5. 결과 저장 (Write Back)  
{{< /callout >}}  

## **명령어 파이프라이닝**   
**(Instruction Pipelining)**  
한 번에 하나의 명령어만 실행하는 것이 아니라 하나의 명령어가 실행되는 도중에 다른 명령어 실행을 시작하는 식으로 동시에 여러 개의 명령어를 실행하는 기법  

### **파이프라인 위험**  
**(Pipeline hazard)**  
명령어 파이프라이닝이 전체적인 성능 향상을 제공하지만 특정 상황에서 실패하는 경우도 있음  

#### **데이터 위험 (Data Hazard)**  
명령어 간 '데이터 의존성'에 의해 발생  
=> 명령어의 실행 결과가 다음 명령어의 실행에 영향을 미치는 경우 발생  

{{< callout type="info" >}}  
**모든 명령어를 동시에 처리할 수 없음**   
명령어 1 = R1 <- R2 + R3  
명령어 2 = R4 <- R1 + R5  
=> 이전 명령어를 끝까지 실행해야만 비로소 실행  
{{< /callout >}}  

#### **제어 위험 (Control Hazard)**  
분기 등으로 인한 '프로그램 카운터의 갑작스러운 변화'에 의해 발생  
=> 프로그램 카운터가 JUMP 등으로 인해 메모리 번지를 갑자기 옮겼을 때 그동안 진행되고 있던 다음 명령어들이 쓸모없게 되는 경우 발생  

{{< callout type="info" >}}  
**분기 예측**  
제어 위험을 막기 위해 미리 프로그램 카운터의 다음 값을 예측 함  
=> 프로그램이 어디로 분기할지 미리 예측  
{{< /callout >}}  

#### **구조적 위험 (Structural Hazard)**  
**(= 자원 위험 (Resource fazard))**  
명령어를 겹쳐 실행하는 과정에서 서로 다른 명령어가 동시에 ALU, 레지스터 등과 같은 CPU 부품을 사용하려고 할 때 발생  

<br>
<hr>

## **슈퍼스칼라**
**(SuperScalar)**  
CPU 내부에 여러 개의 명령어 파이프라인을 포함한 구조  
(오늘날의 멀티스레드 프로세서 (하드웨어적 스레드))  
=> 슈퍼스칼라 프로세스는 매 클럭 주기마다 동시에 여러 명령어를 인출할 수도, 실행할 수도 있어야 함  

{{< callout type="info" >}}  
**슈퍼스칼라 프로제서/CPU**  
슈퍼스칼라 구조로 명령어 처리가 가능한 CPU  

**이론적**  
슈퍼스칼라 프로세서는 파이프라인 개수에 비례하여 프로그램 처리 속도가 증가  

**BUT**  
파이프라인 위험 등의 예상치 못한 문제로 인해 실제로는 파이프라인 개수에 비례하여 프로그램 처리 속도가 증가하지는 않음  

=> 이 때문에 슈퍼스칼라 방식을 차용한 CPU는 파이프라인 위험을 방지하기 위해 고도로 설계되어야 함  
(여러 개의 파이프라인을 이용하면 하나의 파이프라인을 사용할 때보다 데이터 위험, 제어 위험, 자원 위험을 피하기 더욱 까다롭기 때문)  
{{< /callout >}}  

<br>
<hr>

## **비순차적 명령어 처리**  
**(OoOE : Out-of-Order Execution)**  
파이프라인의 중단을 방지하기 위해 명령어를 순차적으로 처리하지 않는 명령어 병렬 처리 기법   
(오늘날 CPU 성능 향상에 크게 기여한 기법, 대부분의 CPU가 차용하는 기법)  

{{< callout type="info" >}}  
의존성이 없는 명령어의 순서를 바꿔서 파이프라이닝을 최대로 활용  
=> 의존성을 고려하여 순서를 바꿈  
=> 전체 프로그램 실행 흐름에 영향이 없는 경우에만 가능  
{{< /callout >}}  

<br>
<hr>

# **ISA, CISC, RISC**
파이프라이닝에 유리한 명령어  

## **명령어 집합**  
**(Instruction Set)**  
특정 컴퓨터 아키텍처나 프로세서가 이해하고 실행할 수 있는 명령어들의 전체 집합을 의미  
(CPU가 이해할 수 있는 명령어들의 모음)  
=> 산술 연산, 메모리 액세스, 제어 흐름 등을 수행하는 명령어들이 명령어 집합에 포함 됨  

<br>

## **명령어 집합 구조**
**(ISA : Instruction Set Architecture)**  
컴퓨터나 프로세서가 이해하고 수행할 수 있는 명령어들의 집합과 이 명령어들을 실행하기 위한 하드웨어적인 구조를 정의  
=> CPU가 어떤 명령어를 이해하는지에 따라 컴퓨터 구조 및 설계 방식이 달라짐  
=> 명령어가 달라지면 명령어 해석 방식, 레지스터의 종류와 개수, 파이프라이닝의 용이성 등이 달라짐  
(ISA는 CPU의 언어이자 하드웨어가 소프트웨어를 어떻게 이해할지에 대한 약속)  

{{< callout type="info" >}}  
(CPU마다 ISA가 다를 수 있음 => 명령어의 세세한 생김새, 연산, 주소 지정 방식 등은 CPU마다 다름)   
{{< /callout >}}  

<br>
<hr>

## **CISC**  
**(Complex Instruction Set Computer)**  
복잡하고 많은 종류의 명령어 집합을 활용하는 컴퓨터(CPU)  
=> 명령어의 형태와 크기가 다양한 '가변 길이 명령어'
(CISC 기반의 ISA = x86, x86-64, ...)  

{{< callout type="info" >}}  
강력한 명령어 활용 = 상대적으로 적은 수의 명령어로도 프로그램 실행 가능  
=> 메모리를 최대한 아끼며 개발해야 했던 시기에는 인기가 높았음  
{{< /callout >}}  

{{< callout type="info" >}}  
**명령어 파이프라인을 구현하는데 불리**  
- 명령어의 크기와 실행되기까지의 시간이 일정하지 않음  
  => 활용하는 명령어가 워낙 복잡하고 다양한 기능을 제공하기 때문  
- 명령어를 실행하는 데에 여러 클럭 주기를 필요로 함  
  => 복잡한 명령어 때문  

> 명령어의 규격화가 어려워 파이프라이닝을 어렵게 만듬  
> => CISA가 활용하는 명령어는 명령어 수행 시간이 길고 가지각색이기 때문에 파이프라인이 효율적으로 명령어를 처리할 수 없음  
> 대다수의 복잡한 명령어는 사용 빈도가 낮음  
> => CISC 명령어 집합이 다양하고 복잡한 기능을 지원하지만 실제로는 자주 사용되는 명령어만 쓰였음  

=> CISC기반의 CPU는 성장에 한계가 있음  
{{< /callout >}}  

<br>
<hr>

## **RISC**  
**(Reduced Instruction Set Computer)**  
짧고 간단한 규격화된 적은 종류의 명령어 집합을 활용하는 컴퓨터(CPU)  
=> 명령어의 형태가 단순하고 동일한 크기를 가지는 '고정 길이 명령어'
(RISC 기반의 ISA = ARM, MIPS, SPARC, ...)  

{{< callout type="info" >}}  
**명령어 파이프라인을 구현하는데 유리**  
- 단순하고 적은 수의 고정 길이 명령어 집합을 활용    
- 메모리 접근 최소화(load, store), 레지스터 십분 활용  

=> 명령어 종류가 CISC보다 적기에 더 많은 명령어로 프로그램을 동작시킴  
{{< /callout >}}  

<br>
<hr>

## **CISC vs RISC**  
|특징| CISC | RICS |
|----|------|------|
|명령어|복잡하고 다양|단순하고 적음|
|명령어 길이|가변 길이 명령어|고정 길이 명령어|
|주소 지정 방식|다양함|적음|
|프로그램을 이루는 명령어의 수|적음|많음|
|명령어 처리 클럭|여러 클럭에 걸쳐 명령어 수행|1클럭 내외로 명령어 수행|
|파이프라이닝 유리/불리|불리|유리|


<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)


