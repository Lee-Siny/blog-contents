---
title: "보조기억장치"
meta_title: "보조기억장치"
description: "HDD, Flash Memory, RAID"
date: 2024-01-12T10:14:42+09:00
image: "/images/cs.svg"
categories: ["Computer-Science"]
author: "Sinyoung Lee"
tags: ["Computer-Science"]
draft: false
---

# **다양한 보조기억장치**
하드디스크, 플레시 메모리(USB 메모리, SD 카드, SSD)  

## **하드디스크**
**(HDD : Hard Disk Srive)**  
자기적인 방식으로 데이터를 저장하는 보조기억장치  
=> 자기 디스크(magnetic disk)의 일종  

### **플래터 (Platter)**  
하드디스크에서 실질적으로 데이터가 저장되는 곳  
=> 일반적으로 양면 모두 사용, 여려 겹 사용 가능  

{{< callout type="info" >}}  
자기 물질로 덮여 있어 수많은 N극과 S극을 저장  
=> N극과 S극은 0과 1의 역할을 수행  
{{< /callout >}}  

### **스핀들 (Spindle)**
플래터를 회전시키는 구성 요소
=> 스핀들이 플래터를 돌리는 속도는 RPM 단위로 표현

{{< callout type="info" >}}  
**(RPM : Revolution Per Minute)**  
분당 회전수  

ex) 15,000 RPM = 1분당 15,000바퀴 회전  
{{< /callout >}}  

### **헤드 (Head)**  
플래터를 대상으로 데이터를 읽고 쓰는 구성 요소  
(플래터의 모든 면 마다 헤드가 디스크 암에 부착되어 있음)  

### **디스크 암 (disk arm)**  
헤드를 원하는 위치로 이동시키는 부품  

<br>

## **플래터에 데이터 저장**  
트랙(track)과 섹터(sector) 단위로 데이터를 저장  

### **트랙 (track)**  
한 플래터를 동심원으로 나눈 공간  

{{< callout type="info" >}}  
**트랙간 갭**  
트랙 사이의 간격 => 트랙간의 자기장 간섭을 방지하기 위한 간격  
{{< /callout >}}  

### **섹터 (sector)**  
트랙에서 나누어진 단위  
(하드 디스크의 가장 작은 전송 단위, 일반적으로 약 512 바이트만큼의 공간)  
=> 하나 이상의 섹터를 묶어 블록 (block)이라고 하기도 함  

{{< callout type="info" >}}  
**섹터간 갭**  
섹터들을 구분하기 위한 간격  
{{< /callout >}}  

### **실린더 (cylinder)**  
여러 겹의 플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위  

{{< callout type="info" >}}  
연속된 정보는 보통 한 실린더에 기록  

같은 트랙이 위치한 곳들에만 저장 (즉, 하나의 실린더에 저장)  
=> 디스크 암을 움직이지 않고도 바로 데이터에 접근할 수 있음  
{{< /callout >}}  

<br>

## **데이터 접근**
하드디스크가 저장된 데이터에 접근하는 시간  
=> 탐색 시간 + 회전 지연 시간 + 전송 시간  

### **탐색 시간 (seek time)**  
접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간  

### **회전 지연 (rotational latency)**  
헤드가 있는 곳으로 플래터를 회전시키는 시간  

### **전송 시간 (transfer time)**  
하드디스크와 컴퓨터 간에 데이터를 전송하는 시간  

{{< callout type="info" >}}  
**단일 헤드 디스크(single-head disk)**  
(이동 헤드 디스크(movable-head disk))  
플래터의 한 면당 헤드가 하나씩 달려있는 하드 디스크  
=> 헤드를 데이터가 있는 곳 까지 움직여야 함  


**다중 헤드 디스크(multiple-head disk)**
(고정 헤드 디스크(fixed-head disk))  
헤드가 트랙별로 여러 개 달려있는 하드 디스크  
=> 헤드를 움직일 필요없음  
{{< /callout >}}  

<br>

## **플래시 메모리**  
전기적으로 데이터를 읽고 쓸 수 있는 반도체 기반의 저장 장치  
(USB 메모리, SD 카드, SSD 등)  

### **셀 (cell)**  
플래시 메모리에서 데이터를 저장하는 가장 작은 단위  

### **페이지 (page)**  
셀들이 모여 만들어진 단위  
=> 플래시 메모리에서 읽기와 쓰기에서 사용되는 단위  

{{< callout type="info" >}}  
**페이지의 상태**  
**Free**  
어떠한 데이터도 저장하고 있지 않아 새로운 데이터를 저장할 수 있는 상태  

**Valid**  
이미 유효한 데이터를 저장하고 있는 상태  
=> 플래시는 덮어쓰기가 불가능하여 Vaild 상태의 페이지에는 저장할 수 없음  

**Invalid**  
유효하지 않은 데이터 (쓰레기 값)를 저장하고 있는 상태  
=> 가비지 컬렉션 (GC - Garbage Collection)을 통해 삭제 진행  


**가비지 컬렉션**
유요한 페이지들만 새로운 블록으로 복사한 후 기존 블록을 삭제하여 공간을 정리하는 기능  
{{< /callout >}}  

### **블록(block)**  
페이지들이 모여 만들어진 단위  
=> 플래시 메모리에서 삭제에서 사용되는 단위  

### **플레인(plane)**  
블록이 모여 만들어진 단위  

### **다이 (die)**  
플레인이 모여 만들어진 단위  

<br>

## **내부 회로 구성방식에 따른 플래시 구분**  

### **NOR형 플래시**  
트랜지스터들이 병렬로 접속된 형태  
=> 어느 한 트랜지스터에 저장된 값만 '1' 이어도 비트 선의 전압은 0V가 되는 NOR 게이트와 같이 동작하는 플래시 메모리  

### **NAND형 플래시**  
모든 트랜지스터들이 직렬로 접속된 형태  
=> 읽고자 하는 트랜지스터에 저장된 값이 '0' 일 경우에 직렬로 접속된 다른 트랜지스터들과는 상관없이 비트 선의 전압은 논리적으로 1이 되는 NAND 게이트와 같이 동작하는 플래시 메모리  

<br>

## **셀 당 저장하는 비트 수에 따른 플래시 구분**  
|  | SLC | MLC | TLC |
|--|-----|-----|-----|
|셀당 bit|1 bit|2 bit|3 bit|
|속도|빠름|보통|느림|
|기록 가능 횟수|100,000회|10,000회|1,000회|
|읽기 속도|빠름|보통|느림|
|쓰기 속도|빠름|보통|느림|
|지우기 속도|빠름|보통|느림|
|안전성|빠름|보통|느림|
|가격|빠름|보통|느림|

### **SLC (single-level cell)**  
한 셀당 한 비트씩 저장하는 셀  
=> 0 또는 1 저장 가능  

{{< callout type="info" >}}  
- MLC, TLC 타입보다 비트의 빠른 입출력 가능  
- MLC, TLC 타입보다 수명이 김  
- 용량 대비 가격이 높음  

=> 데이터 읽고 쓰기가 매우 많이 반복되고 고성능의 빠른 저장장치가 필요한 경우 사용  
{{< /callout >}}  

### **MLC (multiple-level cell)**  
한 셀에 2비트씩 저장할 수 있는 셀  
=> 00, 01, 10, 11 총 4 가지 저장 가능  

{{< callout type="info" >}}  
- SLC보다 느린 입출력  
- SLC보다 짧은 수명   
- SLC보다 가격 대비 저렴  
- SLC보다 대용화 유리  
- 시중에서 많이 사용  

{{< /callout >}}  

### **TLC (triple-level cell)**  
한 셀에 3비트씩 저장할 수 있는 셀  
=> 000, 001, 010, 011, 100, 101, 110, 111 총 8 가지 저장 가능  

{{< callout type="info" >}}  
- MLC보다 느린 입출력  
- MLC보다 짧은 수명   
- MLC보다 가격 대비 저렴  
- MLC보다 대용화 유리  
- 시중에서 많이 사용  

{{< /callout >}}  

<br>
<hr>

# **RAID의 정의와 종류**  

## **RAID**  
**(Redundant Array of Independent Disks)**  
데이터의 안전성, 높은 성능을 위해 여러 물리적 보조기억장치를 마치 하나의 논리적 보조기억장치처럼 사용하는 기술  
=> 다수의 작은 디스크들을 배열로 연결하여 용량, 신뢰성을 높인 대용량 디스크 시스템  
(여러 개의 하드 디스크나 SSD를 마치 하나의 장치처럼 사용)  
=> RAID 구성 방법 = RAID 레벨  

{{< callout type="info" >}}  
긱 RAID 래밸마다 장단점이 있어 어떤 상황에서 무엇을 최우선으로 원하는지에 따라 죄적의 RAID 레벨이 달라질 수 있음  
{{< /callout >}}  

### **RAID 0**  
여러 개의 보조기억장치에 데이터를 단순히 분산하여 저장하는 방식 (병렬로 분산)  
=> 데이터를 저장할 때 각 하드디스크가 번갈아가며 데이터를 저장  
(저장되는 데이터가 하드 디스크 개수만큼 나뉘어 저장됨)  

{{< callout type="info" >}}  
=> 구성된 하드 디스크 중 1개라도 문제가 생기면 다른 하드 디스크의 정보를 읽는데 문제가 발생하는 구조  
{{< /callout >}}  

{{< callout type="info" >}}  
**스트라이핑 (striping)**  
분산하여 저장하는 것  

**스트라입 (stripe)**  
줄무늬처럼 분산되어 저장된 데이터 
{{< /callout >}}  
 
### **RAID 1**  
데이터를 두 개의 디스크들에 중복 저장하는 방식  
(RAID-0 의 단점을 보완)  
=> 거울처럼 완벽한 복사본을 만드는 구성으로 디스크 미러링(disk mirroring)방식 이라고도 함  
=> 데이터를 쓸 때 원본과 복사본 두 곳에 씀 (RAID 0보다 쓰기 속도 느림)  

{{< callout type="info" >}}  
복구가 매우 간단  
=> 미러 디스크가 존재하기 때문에 하나에 문제가 발생해도 잃어버린 정보를 금방 되찾을 수 있음  

하드디스크 갯수가 한정되었을 때 사용 가능한 용량이 적어짐  
=> 복사본이 만들어지는 용량만큼 사용 불가
=> 많은 양의 하드 디스크 필요 => 비용 증가
{{< /callout >}}  

### **RAID 4**  
오류를 검출하고 복구하기 위한 정보를 저장하는 디스크(패리티 디스크)를 추가한 방식  
=> 완전한 복사본을 만드는 대신 오류를 검출하고 복구하기 위한 정보를 저장한 장치를 두는 구성 방식

{{< callout type="info" >}}  
적은 하드 디스크로 데이터를 안전하게 보관할 수 있는 방식  
=> 패리티 디스크를 통해서 오류 검출과 복구 가능  

새로운 데이터를 저장할 때마다 패리티 디스크에 접근함으로 병목현상 발생  
=> 새로운 데이터가 저장될 때 마다 패리티 비트를 저장하는 디스크에도 데이터를 쓰게 되기 때문  
{{< /callout >}}  

{{< callout type="info" >}}  
**패리티 비트 (parrity bit)**  
오류를 검출하고 복구하기 위한 정보  

**패리티 디스크 (parrity disk)**  
패리티 비트가 저장되어 있는 디스크  
{{< /callout >}}  

### **RAID 5**  
패리티 정보를 분산하여 저장하는 방식으로 병목현상을 해소한 방식  
=> 패리티 비트를 여러 디스크에 분산배치 하여 병목현상을 해소  

### **RAID 6**   
서로 다른 두 개의 패리티를 배치하여 데이터의 신뢰성을 높인 방식   
=> 패리티가 각 데이터마다 2개씩 존재하여 데이터의 신뢰성이 높음  
=> 데이터를 저장할 때 각 패리티에 접근해야 함으로 쓰기 속도가 저하됨  

### **Nested RAID**   
여러 RAID 레벨을 혼합한 방식  

{{< callout type="info" >}}  
RAID 0 + RAID 1 = RAID 10  
RAID 0 + RAID 5 = RAID 50  
...  
{{< /callout >}}  

<br>
<hr>

> 참고  
> [혼자 공부하는 컴퓨터 구조+운영체제 (책)](https://hongong.hanbit.co.kr/%EC%BB%B4%ED%93%A8%ED%84%B0-%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C/)  
> [혼자 공부하는 컴퓨터 구조+운영체제 (강의)](https://www.inflearn.com/course/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0%EA%B5%AC%EC%A1%B0-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C)


