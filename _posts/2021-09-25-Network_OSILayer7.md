---
title: "Network - OSI 7 Layer && TCP/IP model"
categories:
  - Network
tags:
  - Network
---

## Layer1 (Physical Layer)
- 두 대의 컴퓨터가 통신하려면?
  - 모든 파일과 프로그램은 0과 1의 나열이다.
  - 결국 0과 1만 주고받을 수 있으면 된다.

  - 두대의 컴퓨터를 전선 하나로 연결한다고 상상해보자
  - cf ) 주파수 : 1초당 파동이 진동한 횟수 [단위 : *Hz (헤르츠)*]
  - 아날로그 신호 : 전류의 주파수나 진폭 등 연속적으로 변화하는 형태
  - 디지털 신호 : 0(전류가 흐르지 않는 상태)과 1(전류가 흐르는 상태)의 나열

>  Physical Layer?


  - **0과 1의 나열을 아날로그 신호로 바꾸어 전선으로 흘려 보내고 (encoding)**
  - **아날로그 신호가 들어오면 0과 1의 나열로 해석하여 (decoding)**
  - **물리적으로 연결된 두 대의 컴퓨터가 0과1의 나열을 주고받을 수 있게해주는 module**

- Physical Layer 인코딩/디코딩
  - 데이터를 보내는 컴퓨터 > 1계층 encoder에서 디지털 신호를 아날로그 신호로 변조
  - 변조된 아날로그신호는 전선을타고 데이터를 받는 컴퓨터의 1계층으로 보내짐
  - 데이터를 받는 컴퓨터 > 1계층 decoder에서 아날로그 신호를 디지털 신호로 변조

- Physical Layer기술은 어디에 구현되어있을까?
  - PHY 칩
  - 하드웨어적 구현


## Layer2 (Data-Link Layer)
- ? 여러대의 컴퓨터가 통신하려면 ? 
  - 여러대의 컴퓨터는 전선으로 연결되어있어야합니다.
  - 여러대의 컴퓨터를 하나의 전선으로 묶어서 컴퓨터끼리의 통신을 조절하는 장치를 **스위치**
  - 각각의 스위치와 컴퓨터는 하나의 네트워크 망을 이루고 하나의 네트워크에서 다른 네트워크로 통신을 가능하게하는 장치는 **라우터(공유기)**
  - 라우터와 라우터끼리도 연결시킬 수 있음 --> 이런식으로 전세계의 컴퓨터를 연결한 것을 **인터넷**

>  Data Link Layer?


  - 여러대의 컴퓨터가 지금 내 컴퓨터로 신호를 보내는 경우? 데이터를 어떻게 끊어 읽을 것인가?
  - 잘못 끊어 신호를 잘못인식하는 것을 방지하기 위해서 송신자는 데이터의 앞 뒤에 특정한 비트열을 붙입니다.
  
  - **같은 네트워크에 있는 여러대의 컴퓨터들이 데이터를 주고 받기 위해서 필요한 모듈**
  - Framing은 Data-link Layer에 속하는 작업들 중 하나
    - Fraiming : 데이터의 앞 뒤에 신호의 시작과 끝을 알리는 비트열을 붙이는 작업
  
- Data-Link Layer 데이터 흐름
  - 1) 데이터를 보내는 컴퓨터 > data -> 2계층 encoder -> `1111 data 0000`
    - 시작과 끝을 알리는 비트열과 함께 있는 데이터가 2계층 encoder 에서 만들어짐
  - 2) 데이터는 1계층 인코더를 타서 > 아날로그 신호로 변조 > 전선을 타서 >  데이터를 받는 컴퓨터의 1계층 decoder
  - 3) 데이터를 받는 컴퓨터의 2계층 decoder를 거쳐서 앞 뒤 시작/끝 비트를 제거하고 -> `data` 만추출됨

- Data-link Layer 기술은 어디에 구현되어 있을까?
  - 랜카드
  - 하드웨어적으로 구현

## Layer3 (Network Layer)
- 각 컴퓨터들의 고유한 주소값 : IP주소
- A컴퓨터가 다른 네트워크에 속한 B컴퓨터에게 데이터를 보내기 위해서는 B의 IP주소를 알아야함
- 따라서 전송시그널은 `55.10.54.75 + data` 패킷을 실어서 메시지를 B컴퓨터로 전달.
- `55.10.54.75(IP주소) + data` : 패킷
- A컴퓨터가 B컴퓨터로 데이터를 보낼 때 IP주소를 보고 어떤 네트워크망으로 데이터를 전달할지 판단하는 방법에 대해서 자세히 알고 싶으면 **라우팅**을 공부할 것

> Network Layer


- **수많은 네트워크의 연결로 이루어지는 inter-network 속에서 어딘가에 있는 목적지 컴퓨터로 데이터를 전송하기 위해 IP주소를 이용해서 길을 찾고(routing) 자신 다음의 라우터에게 데이터를 넘겨주는 것(forwarding)**

- Network Layer 기술은 어디에 구현되어있을까?
  - 운영체제의 kernel에 소프트웨어적으로 구현되어있다.

## Layer4 (Transport Layer)
- 데이터를 받는 수신자는 전 세계의 컴퓨터로부터 데이터를 받을 것
- 데이터를 받은 컴퓨터는 여러개의 데이터를 실행중인 프로세스들에게 나누어주려고함
  - 프로세스 A : messenger App
  - 프로세스 B : delivery App
- 어떤 데이터를 무슨 프로세스에게주어야할지 컴퓨터는 어떻게 알 수 있나?
  - By **port number** : 포트번호는 하나의 컴퓨터에서 동시에 실행되고 있는 프로세스들이 서로 겹치지 않게 가져야하는 정수값
  
- 송신자는 데이터를 보낼 때 데이터를 받을 수신자 컴퓨터에 있는 프로세스의 포트번호를 붙여서 보냄

> Transport Layer


- **port 번호를 사용하여 도착지 컴퓨터의 최종 도착지인 process에 까지 데이터가 도달하게 하는 모듈**


- Transport Layer 기술은 어디에 구현되어있을까?
  - 운영체제의 kernel에 소프트웨어적으로 구현되어있다.

## Layer5 (Session Layer)
## Layer6 (Presentation Layer)
## Layer7 (Application Layer)

### OSI vs. TCP/IP 모델
- 사실 현대의 인터넷은 OSI모델이 아니라 TCP/IP 모델을 따로고 있습니다
- TCP/IP모델도 OSI 모델과 마찬가지로 네트워크 시스템에 대한 모델
- 현대의 인터넷이 TCP/IP모델을 따르는 이유는 OSI모델이 TCP/IP 모델과의 시자점유싸움에서 졌기 때문입니다.

- TCP/IP 모델도 1,2,3,4 계층은 OSI와 같음
- TCP/IP Layer5는 Application 계층으로 합쳐짐

- cf) TCP/IP 소켓 프로그래밍 (네트워크 프로그래밍)
  - 운영체제의 Transport layer에서 제공하는 API를 활용해서 통신가능한 프로그래밍을 만드는 것
- cf) 대표적인 Application Layer 프로토콜  : HTTP

> Application Layer


- **The application layer is the highest abstraction layer of the TCP/IP model that provides the interfaces and protocols needed by the users.**
- HTTP, FTP, SMTP 등 응용프로그램들이 네트워크를 사용하기 위한 인터페이스를 제공
