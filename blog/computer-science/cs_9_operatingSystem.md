---
title: "운영체제 시작하기"
meta_title: "운영체제 시작하기"
description: "Operating System, Kernel, Dual Mode, System Call"
date: 2024-01-26T10:48:27+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **운영체제를 알아야 하는 이유**  
데스크톱 컴퓨터, 노트북, 스마트폰에는 모두 운영체제가 설치되어 있음  
ex) window, macOS, linux, android, iOS, ...  

=> 컴퓨터 부품들은 운영체제라는 특별한 프로그램의 지휘하에 작동  
=> 컴퓨터 부품들을 관리하고, 개발한 프로그램들이 올바르게 실행되도록 도움  

<br>

## **운영체제란**  
**Operating System**  
응용 프로그램과 하드웨어 사이에서 실행할 응용 프로그램에 필요한 자원을 할당하고, 응용 프로그램이 올바르게 실행되도록 관리 특별한 프로그램  
=> 메모리 내 커널 영역에 적재  

{{< callout type="info" >}}  
모든 프로그램은 하드웨어를 필요로 함  

ex) 1+2를 계산하는 프로그램 = CPU를 필요로 함  
ex) 이미지를 하드디스크에 저장하는 프로그램 = 하드디스크를 필요로 함  
{{< /callout >}}  

{{< callout type="info" >}}  
**시스템 자원 / 자원**  
프로그램 실행에 마땅히 필요한 요소  
(CPU, 메모리, 보조기억장치, 입출력장치 등과 같은 컴퓨터 부품들은 모두 자원이라 볼 수 있음)  

=> 즉, 모든 프로그램은 실행되기 위해 반드시 자원이 필요    
{{< /callout >}}  

<br>

### **커널 영역 (kernel space)**  
메모리 공간에서 사용자 영역(user space)를 제외한 영역  

{{< callout type="info" >}}  
운영체제는 다른 프로그램을 위한 프로그램이므로 다른 프로그램과 마찬가지로 메모리에 적재되어야함  
=> 운영체제는 특별한 프로그램이므로 항상 컴퓨터 부팅시 메모리내 커널 영역이라는 공간에 따로 적재되어 실행됨  
{{< /callout >}}  

<br>

### **사용자 영역 (user space)**  
메모리 공간에서 사용자가 이용하는 응용 프로그램이 적재되는 영역  
=> 스택 영역, 힙 영역, 데이터 영역, 코드 영역이 사용자 영역에 포함됨  

<br>

### **역할**  
**메모리 관리**  
운영체제는 사용자 영역(메모리)에 실행할 프로그램을 메모리 주소가 겹치지 않도록 적당한 공간에 프로그램들을 적재하고, 더 이상 실행되지 않는 프로그램을 메모리에 삭제하며 지속적으로 메모리 자원을 관리  

**CPU 자원 할당**  
여러개의 응용프로그램이 실행되려면 CPU가 필요, 어느 한 프로그램이 CPU를 독점하면 다른 프로그램들은 올바르게 실행될 수 없기 때문에 운영체제는 최대한 공정하게 여러 프로그램에 CPU 자원을 할당  

=> 운영체제는 응용 프로그램에 자원을 효율적으로 배분하고, 실행할 프로그램들이 지켜야 할 규칙을 만들어 컴퓨터 시스템 전체를 관리함  
=> 운영체제는 관리할 자원별로 기능이 나누어져 있음 (ex. CPU, 메모리, 하드디스크 관리)  

<hr>

## **운영체제를 알아야 하는 이유**  
운영체제가 없다면 간단한 프로그램 동작시에도 하드웨어를 조작하는 코드를 개발자가 모두 직접 작성해야함  
=> 운영체제는 하드웨어를 조작하고 관리하는 기능들을 제공하기 때문에 개발자가 하드웨어 조작 코드를 직접 작성할 필요가 없음  

1.  운영체제는 현재 하드웨어의 상태를 알고 있음  
2.  내가 작성한 코드가 어떻게 실행되었는지를 알고 있음  
3.  하드웨어 상에서 어떤 문제가 발생했는지 알려줌  

=> 운영체제를 깊이 이해하면 운영체제에게 제대로 명령할 수 있게 됨  
=> 하드웨어와 프로그램을 더 깊이 이해할 수 있음 (= 문제해결의 실마리를 찾을 수 있음)  

<br>
<hr>

# **운영체제의 큰 그림**  
운영체제는 사용자를 위한 프로그램이 아닌 사용자가 실행하는 프로그램을 위한 프로그램  
=> 사용자가 실행하는 응용 프로그램이 올바르게 실행되도록 돕고 필요한 자원을 할당해 주는 프로그램  

<hr>

## **운영체제의 심장, 커널**  
운영체제는 현존하는 프로그램 중 규모가 가장 큰 프로그램 중 하나  
ex) 대표적인 운영체제인 리눅스를 구성하는 소스 코드는 천만줄이 넘음  
=> 운영체제가 다양함 = 운영체제 서비스 또한 매우 다양  

<br>

### **커널 (kernel)**
운영체제의 핵심 서비스를 담당하는 부분  

**핵심 서비스**  
- 자원에 접근하고 조작하는 기능  
- 프로그램이 올바르고 안전하게 실행되게 하는 기능  

{{< callout type="info" >}}  
운영체제가 설치된 모든 기기에는 커널이 있음  
=> 어떤 커널을 사용하는지에 따라 컴퓨터 전체의 성능도 달라질 수 있음  
{{< /callout >}}  

{{< callout type="info" >}}  
**운영체제가 제공하는 서비스 중 커널에 포함되지 않는 서비스**  

**사용자 인터페이스(UI, user interface)**  
대표적으로 커널에 포함되지 않는 운영체제가 제공하는 서비스  
=> 윈도우의 바탕화면과 같이 사용자가 컴퓨터와 상호작용할 수 있는 통로  
- 그래픽 유저 인터페이스(GUI, graphical user interface): 화면과 같은 그래픽 기반으로 컴퓨터와 상호작용  
  => 마우스 이용하여 다양한 프로그램 실행, 앱을 터치하여 실행 등 모두 그래픽 유저 인터페이스를 지원하기 때문에 가능  
- 커멘드 라인 인터페이스(CLI, command line interface): 명령어를 입력함으로써 컴퓨터와 상호작용  
  => 아이콘이나 다채로운 화면 없이 정해진 명령어를 입력함으로써 컴퓨터와 상호작용을 수행  

=> 사용자 인터페이스는 운영체제가 제공하는 서비스이지만, 이는 그저 컴퓨터와 상호작용하기 위한 통로일 뿐 커널에 속한 기능은 아님  
=> 실제로 같은 커널을 사용하더라도 사용자 인터페이스는 다를 수 있음  
{{< /callout >}}  

<hr>

## **이중모드와 시스템 호출**  
운영체제는 사용자가 실행하는 응용 프로그램이 하드웨어 자원에 직접 접근하는 것을 방지하여 자원을 보호  
(운영체제는 오직 자신만을 이용하여 자원에 접근할 수 있도록 제어)  
=> 응용 프로그램이 자원에 접근하기 위해서는 운영체제에 도움을 요청  
=> 응용 프로그램의 요청을 받은 운영체제는 응용 프로그램 대신 자원에 접근하여 요청한 작업을 수행  

### **이중 모드 (Dual Mode)**  
CPU가 명령어를 실행하는 모드를 사용자 모드와 커널 모드로 구분하는 방식  
=> 운영체제의 문지기 역할은 이중 모드 로써 구현  

{{< callout type="info" >}}  
CPU가 사용자 모드로 실행 중인지, 커널 모드로 실행중인지는 플래그 레지스터 속 슈퍼바이저 플래그를 보면 알 수 있음  
{{< /callout >}}  

#### **사용자 모드(User Mode)**  
운영체제 서비스를 제공받을 수 없는 실행 모드  
=> 커널 영역의 코드 실행 불가  

{{< callout type="info" >}}  
일반적인 응용 프로그램은 기본적으로 사용자 모드로 실행, 사용자 모드로 실행중인 CPU는 입출력 명령어와 같이 하드웨어 자원에 접근하는 명령어를 실행할 수 없음  
=> 일반적인 응용 프로그램은 사용자 모드로 실행되기 때문에 자원에 접근할 수 없음  
{{< /callout >}}  

#### **커널 모드 (Kernel Mode)**  
운영체제 서비스를 제공받을 수 있는 실행 모드  
=> 커널 영역의 코드 실행 가능  

{{< callout type="info" >}}  
CPU가 커널 모드로 명령어를 실행하면 자원에 접근하는 명령어를 비롯한 모든 명령어를 실행할 수 있음  
=> 운영체제는 커널 모드로 실행되기 때문에 자원에 접근할 수 있음  
{{< /callout >}}  

#### **시스템 호출 (System Call)**  
사용자 모드로 실행되는 프로그램이 운영체제 서비스를 제공받기 위해 커널 모드로 전환하는 요청  
=> 사용자 모드로 실행되는 프로그램은 시스템 호출을 통해 커널 모드로 전환하여 운영체제 서비스를 제공받을 수 있음  
=> 소프트웨어 인터럽트에 포함  

{{< callout type="info" >}}  
**CPU의 시스템 호출 처리 순서**  
1. 시스템 호출 발생 명령어 실행  
2. CPU가 지금까지의 작업을 백업  
3. 커널 영역 내에 시스템 호출을 수행하는 코드(인터럽트 서비스 루틴)을 실행  
4. 기존에 실행하던 응용 프로그램 복귀 후 실행을 계속해 나감  

**시스템 호출 작동 예**  
한 응용프로그램이 하드디스크에 데이터를 저장하는 과정  
(사용자 모드로 실행되는 동안에는 자원(하드디스크)에 접근할 수 없기에 커널 모드로 전환)  
1. 하드디스크에 데이터를 저장하는 시스템 호출을 발생시켜 커널 모드로 전환  
2. 운영체제 내의 '하드 디스크에 데이터를 저장하는 코드'를 실핼함으로써 하드디스크에 접근  
3. 하드디스크에 접근이 끝났다면 다시 사용자 모드로 복귀하여 실행을 계속헤 나감  

{{< /callout >}}  

<br>

## **운영체제의 핵심 서비스**  
프로세스 관리, 자원 접근 및 할당, 파일 시스템 관리  

<br>

### **프로세스 관리**  
**프로세스(process)**  
실행 중인 프로그램  
=> CPU는 한 번에 하나의 프로세스만 실행할 수 있기 때문에 여러 프로세스들을 번갈아 가며 실행 (각 프로세스는 상태도 사용하고자 하는 자원도 다름)  

**운영체제는 다양한 프로세스를 관리하고 실행할 수 있어야 함**  
- 여러 프로세스가 동시에 실행되는 환경에서는 프로세스 동기화  
- 프로세스가 꼼짝도 못하고 더 이상 실행되지 못하는 교착 상태 해결 필요  

{{< callout type="info" >}}  
컴퓨터를 사용하는 동안 메모리 안에서는 새로운 프로세스들이 마구 생성되고, 사용되지 않는 프로세스는 메모리에서 삭제됨  
=> 일반적으로 하나의 CPU는 한 번에 하나의 프로세스만 실행할 수 있기에 CPU는 이 프로세스들을 조금씩 번갈아 가며 실행함  
=> 한 프로세스를 실행하다가 다른 프로세스로 실행을 전환하고, 그 프로세스를 실행하다가 또 다른 프로세스로 실행을 전환하는 것을 반복  
{{< /callout >}}  

<br>

### **자원 접근 및 할당**  
운영체제는 프로세스들이 사용할 자원에 접근하고 조작함으로써 프로세스에 필요한 자원을 할당  
=> 모든 프로세스는 실행을 위해 자원을 필요로함  

#### **CPU**  
운영체제는 프로세스들에 공정하게 CPU를 할당하기 위해 어떤 프로세드부터 CPU를 이용하게 할 것 인지, 얼마나 오래 이용하게 할 것인지 CPU 스케줄링을 통해 할당  
=> 일반적으로 메모리에는 여러 프로세스가 적재되고, 하나의 CPU는 한 번에 하나의 프로세스만 실행 할 수 있음  
=> 하나의 프로세스가 CPU를 이용하고 있다면 다른 프로세스는 기다려야 함  

**CPU 스케줄링**  
운영체제가 프로세스들에 공정하게 CPU를 할당하기 위해 어떤 프로세스부터 CPU를 이용하게 할 것인지 얼마나 오래 CPU를 이용하게 할 것인지를 결정하는 것  

#### **메모리**  
메모리에 적재된 프로세스들은 크기도, 적재되는 주소도 다름 (같은 프로세스라 할지라도 실행시마다 적재 주소 달라짐) 
=> 운영체제는 새로운 프로세스 적재시마다 어느 주소에 적재해야 할지를 결정해야 함  

#### **입출력장치**  
인터럽트 서비스 루틴은 운영체제가 제공하는 기능으로 커널 영역에 있음  (입출력장치가 발생시키는 하드웨어 인터럽트도 마찬가지)  
=> 운영체제는 인터럽트 서비스 루틴(인터럽트를 처리하는 프로그램)을 제공함으로써 입출력 작업을 수행  

<br>

### **파일 시스템 관리**  
운영체제는 보조기억장치 속 데이터를 파일과 디렉터리로 관리  

<hr>

## **가상 머신과 이중 모드의 발전**  
**가상 머신 (Virtual Machine)**  
소프트웨어가 만들어낸 가상 컴퓨터, 새로운 운영체제와 응용 프로그램을 설치하고 실행할 수 있음  
=> 가상 머신 또한 응용 프로그램임
=> 가상 머신에서 실행된 응용 프로그램은 하이퍼바이저 모드로 실행되어 운영체제 서비스를 받도록 할 수 있음  

<hr>

## **시스템 호출의 종류**  
| 종류 | 시스템 호출 | 설명 |
| --- | --- | --- |
| 프로세스 관리 | fork() | 새 자식 프로세스 생성 |
|   | execve() | 프로세스 실행(메모리 공간을 새로운 프로그램의 내용으로 덮어씌움) |
|   | exit() | 프로세스 종료 |
|   | waitpid() | 자식 프로세스가 종료할 때 까지 대기 |
| 파일 관리 | open() | 파일 열기 |
|   | close() | 파일 닫기 |
|   | read() | 파일 읽기 |
|   | write() | 파일 쓰기 |
|   | stat() | 파일 정보 획득 |
| 디렉터리 관리 | chdir() | 작업 디렉터리 변경 |
|   | mkdir() | 디렉터리 생성 |
|   | rmdir() | 비어 있는 디렉터리삭제 |
| 파일 시스템 관리 | mount() | 파일 시스템 마운트 |
|   | umount() | 파일 시스템 마운트 해제 |


<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)


