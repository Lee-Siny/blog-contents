---
title: "프로세스와 스레드"
meta_title: "프로세스와 스레드"
description: "Process, Thread"
date: 2024-02-02T09:58:49+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **프로세스 개요**  
**프로세스 (Process)**  
실행중인 프로그램  

{{< notice "note" >}}  
프로그램은 실행되기 전에 그저 보조기억장치에 있는 데이터 덩어리일 뿐임  
보저기억 장치에 저장된 프로그램을 메모리에 적재하고 실행하는 순간 그 프로그램은 프로세스가 됨  
=> 이러한 과정을 '프로세스를 생성한다'라고 표현  
{{< /notice >}}  

<br>  

## **프로세스 직접 확인하기**  
**Unix**  
ps 명령어로 확인 가능  

**Windows**  
작업 관리자의 프로세스 탭에서 확인가능  

### **포그라운드 프로세스 (forground process)**  
사용자가 보는 앞에서 실행되는 프로세스  
=> 사용자가 볼 수 있는 공간에서 실행되는 프로세스, 사용자가 직접 실행한 프로세스  

### **백그라운드 프로세스 (background process)**  
사용자가 보지 못하는 뒤편에서 실행되는 프로세스  
=> 사용자가 볼 수 없는 공간에서 실행되는 프로세스, 사용자가 실행하지 않는 알 수 없는 프로세스  

{{< notice "info" >}}  
백그라운드 프로세스 중에는 사용자와 직접 상호작용할 수 있는 프로세스와 상호작용하지 않고 정해진 일만 수행하는 프로세스가 존재 (데몬, 서비스)  

**데몬 (demon)**  
유닉스 체계의 운영체제에서 백그라운드 프로세스를 부르는 명칭  

**서비스 (service)**  
윈도우 운영체제에서 백그라운드 프로세스를 부르는 명칭  
{{< /notice >}}  

<br>

## **프로세스 제어 블록**  












<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)


