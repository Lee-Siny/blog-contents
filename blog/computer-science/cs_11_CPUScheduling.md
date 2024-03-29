---
title: "CPU 스케줄링"
meta_title: "CPU 스케줄링"
description: "CPU 스케줄링, 우선순위, CPU 스케줄링 알고리즘"
date: 2024-02-08T13:48:31+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **CPU 스케쥴링 개요**  
**CPU 스케줄링 (CPU scheduling)**  
운영체제가 프로세스들에게 공정하고 합리적으로 CPU 자원을 배분하는 것  
=> 프로세스들에게 공정하고 합리적으로 CPU 자원을 할당하기 위해 운영체제는 어떤 프로세스에 CPU를 할당할지, 어떤 프로세스를 기다리게 할지를 결정  

{{< callout type="info" >}}  
**CPU 스케줄링은 컴퓨터 성능과 직결**  
현명하게 CPU 배분하지 않을 경우 반드시 실행해야 할 프로세스들이 실행되지 못하거나, 당장 급하지 않은 프로세스들만 주로 실행되는 등 무질서한 상태가 발생할 수도 있기 때문  
{{< /callout >}}  

<br>

## **프로세스 우선순위**  
운영체제는 프로세스의 중요도에 맞게 CPU를 이용할 수 있게 우선순위(priority)를 부여  

### **입출력 집중 프로세스 (I/O bound process)**  
비디오 재생이나 디스크 백업 작업을 담당하는 프로세스와 같이 입출력 작업이 많은 프로세스 (비디오 재생, 디스크 백업 등)  
=> 실행 상태보다는 입출력을 위한 대기상태에 더 많이 머무르게됨  

### **CPU 집중 프로세스 (CPU bound process)**  
복잡한 수학 연산, 컴파일, 그래픽 처리 작업을 담당하는 프로세스와 같이 CPU 작업이 많은 프로세스 (복잡한 연산, 컴파일, 그래픽 처리 등)   
=> 대기 상태보다는 실행 상태에 더 많이 머무르게 됨  

### **입출력 작업이 많은 프로세스가 우선순위간 높은 이유**  
CPU 집중 프로세스는 CPU를 많이 사용해야 하는 프로세스, 입출력 집중 프로세스는 CPU를 많이 사용하지 않는 프로세스  
=> CPU 집중 프로세스와 입출력 집중 프로세스가 모두 동일한 빈도로 CPU 를 사용하는 것은 비합리적  

{{< callout type="info" >}}  
CPU 집중 프로세스와 입출력 집중 프로세스가 동시에 CPU 자원을 요구했다고 가정  
=> 입출력 집중 프로세스를 가능한 한 빨리 실행시켜 입출력장치를 끊임없이 작동시키고, 그 다음 CPU 집중 프로세스에 집중적으로 CPU를 할당하는 것이 더 효율적  

입출력장치가 입출력 작업을 완료하기 전까지는 입출력 집중 프로세스는 어차피 대기 상태가 될 예정이기 떄문에 입출력 집중 프로세스를 얼른 먼저 처리해버리면 다른 프로세스가 CPU를 사용할 수 있기 때문  
{{< /callout >}}  

{{< callout type="info" >}}  
- 상황과 프로세스 중요도에 맞게 프로세스가 CPU를 쓸 수 있게 하기 위해 OS는 프로세스마다 우선순위를 부여  
- OS는 각 프로세스의 PCB에 우선순위를 명시하고 PCB의 우선순위를 기준으로 먼저 처리할 프로세스를 결정  
- 우선순위가 높다고 무조건 먼저 실행되는 것은 아니지만 더 빨리 더 자주 실행될 가능성이 높음  

{{< /callout >}}  

#### **CPU 버스트와 입출력 버스트**  
CPU를 이용하는 작업 = CPU 버스트 (CPU burst)  
입출력 장치를 기다리는 작업 = 입출력 버스트 (I/O burst)  

=> 프로세스는 일반적으로 CPU 버스트와 입출력 버스트를 반복하며 실행됨  
= CPU 집중 프로세스는 CPU 버스트가 많은 프로세스  
= 입출력 집중 프로세스는 입출력 버스트가 많은 프로세스  

<br>

## **스케줄링 큐 (scheduling queue)**  
CPU, 메모리, 특정 입출력장치 등을 사용하고 싶은 프로세스들을 줄을 세워 스케줄링 큐로 구현하고 관리 (운영체제가 관리하는 대부분의 자원은 큐로 관리됨)  
=> 큐는 자료 구조 관점에서 보았을 때는 먼저 삽입된 데이터가 먼저 나가는 선입선출(First In First Out) 자료 구조이지만, 스케줄링에서 이야기하는 큐는 반드시 선입선출 방식일 필요는 없음  

{{< callout type="info" >}}  
PCB에 우선순위가 적혀 있지만 CPU를 사용할 다음 프로세스를 찾기 위해 운영체제가 일일이 모든 프로세스의 PCB를 찾는 것은 비효율적  
=> CPU를 원하는 프로세스들은 한 두개가 아니며, CPU를 요구하는 새로운 프로세스는 계속 생겨나기 때문  
(운영체제가 매번 일일이 모든 PCB를 검사하여 먼저 자원을 이용할 프로세스를 결정하는 일은 매우 번거로울 뿐더라 오랜 시간이 걸리는 일)  
{{< /callout >}}  

### **준비 큐 (ready queue)**
CPU를 이용하고 싶은 프로세스들이 서는 줄

### **대기 큐 (waiting queue)**  
입출력장치를 이용하기 위해 대기 상태에 접어든 프로세스들이 서는 줄  

### **스케쥴링 큐 실행**  
**대기 상태**  
1. 같은 장치를 요규한 프로세스들은 같은 대기 큐에서 입출력 작업이 완료되기를 기다림  
2. 입출력이 완료되어 완료 인터럽트가 발생하면 운영체제는 대기 큐에서 작업이 완료된 PCB를 찾고 이 PCB를 준비 상태로 변경한 뒤 대기 큐에서 제거  
  => 준비 상태로 변경 된 PCB는 준비큐로 이동  

**준비 상태**  
1. 준비 상태에 있는 프로세스들의 PCB는 준비 큐의 마지막에 삽입되어 CPU를 사용할 차례를 기다림  
2. 운영체제는 PCB들이 큐에 삽입된 순서대로 프로세스를 하나씩 꺼내어 실행하되, 그중 우선순위가 높은 프로세스를 먼저 실행  
  => 우선순위가 낮은 프로세스들이 먼저 큐에 삽입되었더라도 우선순위가 높은 프로세스는 먼저 처리될 수 있음 (대기상태 프로세스도 동일)  

<br>

## **선점형과 비선점형 스케줄링**  
어떤 프로세스에  CPU를 허락했으나,다른 프로세스가 급하게 당장 사용을 요청할 경우 OS는 두가지 선택을 할 수 있음  
=> CPU를 사용중인 프로세스로부터 빼앗아 바로 할당함 (선점형), 현재 프로세스 작업이 끝날때까지, 급한 프로세스를 기다림 (비선점형)  

### **선점형 스케줄링 (preemptive scheduling)**  
프로세스가 CPU를 비롯한 자원을 사용하고 있더라도 운영체제가 프로세스로부터 자원을 강제로 빼앗아 다른 프로세스에 할당할 수 있는 스케줄링 방식  
=> 어느 하나의 프로세스가 자원 사용을 독점할 수 없는 스케줄링 방식  

{{< callout type="info" >}}  
- 더 급한 프로세스가 언제든 끼어들어 사용할 수 있는 스케줄링 방식이므로 어느 한 프로세스의 자원 독점을 막고 프로세스들에게 골고루 자원을 배분할 수 있음   
  => 어느 한 프로세스의 자원 독점 방지, 모든 프로세스가 골고루 자원 사용 가능  
- 문맥 교환 과정에서 오버헤드 발생할 수 있음  

=> 대부분의 운영체제는 선점형을 차용하고 있음  
{{< /callout >}}  

### **비선점형 스케줄링 (non-preemptive scheduling)**  
프로세스가 자원을 사용하고 있다면 그 프로세스가 종료되거나 스스로 대기상태에 접어들기 전까진 다른 프로세스가 끼어들 수 없는 스케줄링 방식  
=> 하나의 프로세스가 자원 사용을 독점할 수 있는 스케줄링 방식  

{{< callout type="info" >}}  
- 다른 프로세스는 자원을 이용하는 프로세스의 사용이 모두 끝날 때까지 대기해야 함  
  => 어느 한 프로세스의 자원 독점 가능, 모든 프로세스가 골고루 자원 사용 불가  
- 문맥 교환 횟수가 선점형에 비해 적기 때문에 오버헤드 적음  

{{< /callout >}}  

<br>
<hr>

# **CPU 스케줄링 알고리즘**  
운영체제마다 다른 스케줄링 알고리즘을 사용  

## **선입 선처리 스케줄링 (FCFS scheduling)**  
**First Come First Served Scheduling**  
단순히 준비된 큐에 삽입된 순서대로 프로세스들을 처리하는 비선점형 스케줄링  알고리즘  
=> CPU를 먼저 요청한 프로세스부터 CPU를 할당하는 스케줄링 방식  
=> CPU를 오래 사용하는 프로세스가 먼저 들어올 경우, 다른 프로세스들은 무작정 기다려야함  

{{< callout type="info" >}}  
**호위 효과 (conboy effect)**  
짧은 런타임을 가진 프로세스가 긴 런타임을 가진 프로세스의 종료 시간까지 무작정 대기하는 현상  
=> CPU를 오래사용하는 프로세스가 먼저 도착하면 다른 프로세스는 그 프로세스가 사용하는 동안 무작정 기다릴 수 밖에 없음  

ex)  
A(17ms), B(7ms), C(1ms) 순서대로 삽입되었다고 가정,  
C는 1ms 를 실행하기 위해 17 + 7 = 24ms의 시간을 기다려야함  
{{< /callout >}}  

<br>

## **최단 작업 우선 스케줄링 (SJF scheduling)**  
**Shortest Job First Scheduling**  
준비 큐에 삽입된 프로세스들 중 CPU 이용 시간 길이가 가장 짧은 프로세스부터 실행하는 스케줄링 알고리즘  
(호위 효과를 방지하기 위해 가장 짧은 프로세스를 먼저 실행하는 스케줄링 방식)  
=> 비선점형으로 구현되지만 선점형으로 구현될 수도 있음 (비선점형이 Default)  

<br>

## **라운드 로빈 스케줄링 (Round Robin Scheduling)**  
정해진 타임 슬라이스만큼의 시간 동안 돌아가며 CPU를 이용하는 선점형 스케줄링 알고리즘  
(선입 선처리 스케줄링 + 타임 슬라이스)  

{{< callout type="info" >}}  
큐에 삽입된 순서대로 CPU를 정해진 시간만큼만 이용하고, 정해진 시간을 모두 사용했음에도 완료되지 않은 경우 다시 큐의 맨뒤에 삽입  
(프로세스가 교체될 때 문맥 교환이 발생)  
{{< /callout >}}  

{{< callout type="info" >}}  
**타임 슬라이스**  
각 프로세스가 CPU를 사용할 수 있는 정해진 시간  

=> 타임슬라이스가 지나치게 크면 사실상 선입 선처리 스케줄링과 다를바 없어 호위 효과가 생길 수 있음  
=> 타임슬라이스가 지나치게 작으면 문맥 교환에 발생하는 비용이 너무 커짐  
{{< /callout >}}  

<br>

## **최소 잔여 시간 우선 스케줄링 (SRT Scheduling)**  
**Shortest Reamining Scheduling**  
준비 큐에 있는 프로세스들 중에서 현재 실행 중인 프로세스의 남은 실행 시간이 가장 짧은 프로세스를 우선으로 실행하는 선점형 스케줄링 알고리즘   
(최단 작업 우선 스케줄링 알고리즘 + 라운드 로빈 알고리즘)  

{{< callout type="info" >}}  
최소 잔여 시간 스케줄링 하에서 프로세스들은 정해진 타임 슬라이스만큼 CPU를 사용하되, CPU를 사용할 다음 프로세스로는 남아있는 작업시간이 가장 짧은 프로세스가 선택됨  
{{< /callout >}}  

<br>

## **우선순위 스케줄링 (Priority Scheduling)**  
프로세스들에 우선순위를 부여하고, 가장 높은 우선순위를 가진 프로세스로부터 실행하는 스케줄링 알고리즘  
(우선순위가 같은 프로레스들은 선입선처리로 스케쥴링)  

{{< callout type="info" >}}  
**기아 현상 (starvation)**  
우선순위가 낮은 프로세스의 실행이 우선순위가 높은 프로세스에 의해 계속 연기되는 현상  

**에이징 (aging)**  
오랫동안 대기한 프로세스의 우선순위를 점차 높이는 방식  
=> 우선순위가 낮은 스로세스의 실행이 계속 뒤로 밀리는것을 방지하기 위한 기법  
{{< /callout >}}  

<br>

## **다단계 큐 스케줄링 (multilevel queue scheduling)**  
우선순위별로 준비 큐를 여러개 사용하는 스케줄링 방식  
(우선순위 스케줄링의 발전된 형태)  
=> 각 큐는 서로 다른 우선순위 레벨을 가지고 있으며, 각 레벨에 따라 우선순위가 다르게 설정  

{{< callout type="info" >}}  
우선순위가 가장 높은 큐에 있는 프로세스들을 먼저 처리하고, 우선순위가 가장 높은 큐가 비어있는 경우 그 다음 우선순위 큐에 있는 프로세스들을 처리  
=> 큐별로 타임 슬라이스를 여러 개 지정할 수 있고, 큐마다 다른 스케줄링 알고리즘을 사용할 수 있음  
(각 큐별로 프로세스간의 이동이 불가)  
{{< /callout >}}  

<br>

## **다단계 피드백 큐 스케줄링 (multilevel feedback queue scheduling)**  
각 큐별로 프로세스간의 이동이 가능하도록 만든 스케줄링 방식  
(다단계 큐 스케줄링의 발전된 형태, 다단계 큐 스케줄링의 기아 현상을 보완)  
=> 어떤 프로세스의 CPU 이용 시간이 길면 낮은 우선순위 큐로 이동, 어떤 프로세스가 낮은 우선순위 큐에서 너무 오래 기다린다면 높은 우선순위 큐로 이동시킬 수 있는 알고리즘  

{{< callout type="info" >}}  
다단계 피드백 큐 스케줄링 에서 새로 준비 상태가 된 프로세스가 있다면 우선 우선순위가 가장 높은 우선순위 큐에 삽입되고 일정 시간(타임 슬라이스) 동안 실행  
=> 만약 해당 큐에서 실행이 끝나지 않는다면 다음 우선순위 큐에 삽입되어 실행된다. 결국 CPU를 오래 사용해야 하는 프로세스는 점차 우선순위가 낮아짐  

=> 비교적 CPU를 오래 사용해야 하는 프로세스들은 우선순위가 낮아지고, 입출력 집중 프로세스들은 우선순위가 높은 큐에서 실행이 끝남 (기아 현상 예방)  
{{< /callout >}}  

<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)


