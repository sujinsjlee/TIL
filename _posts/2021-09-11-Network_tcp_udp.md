---
title: "Network - TCP UDP"
categories:
  - Network
tags:
  - Network
---

## Transport Layer
> Endpoint 간 **신뢰성** 있는 데이터 **전송**을 담당하는 계층  
> 신뢰성 : 데이터를 순차적, 안정적인 전달  
> 전송 : 포트번호에 해당하는 프로세스에 데이터를 전달  



- 만약에 Transport Layer 가 없다면 ? 
  - 데이터의 순차 전송 원활히 x
    - 송신자 123 --> 수신자 231
  - Flow (흐름 문제)
    - 송수신간의 데이터 처리 속도 차이 
  - Congestion (혼잡 문제)
    - 송신자쪽에서 데이터를 보내도 네트워크가 혼잡하면 시그널을 처리할 수 없음
    
## TCP (Transmission Control Protocol)
> **신뢰성 있는 데이터 통신을 가능하게 해주는 프로토콜**


- 특징 : Connection 연결
  - 3 way-handshake (양방향 통신)
  - 데이터 순차 전송 보장
  - Flow Control
  - Congestion Control (혼잡 제어)
  - Error Detection : by checksum


> **Segment** : protocol 안에서 데이터의 단위  
> application 단에서 tcp layer쪽으로 데이터를 전송하면 layer쪽에서 데이터를 자르고 그 데이터는 segment 단위로 protocol 내부적으로 처리  
> segment = TCP Header + Data  


- TCP Header flag bit
  - ACK : 수신자가 송신자에게 보내는 flag bit
  - SYN : Connection 연결하기 위한 flag bit
  - FIN : Connection 연결을 close 하기 위한 flag bit


### TCP의 데이터 전송방식
- **3 way-handshake**
  - Connection 연결
    - 1) SYN 비트를 1로 설정해 Client -> Server 패킷 송신
    - 2) SYN, ACK 비트를 1로 설정해 Server -> Client 패킷 송신
    - 3) ACK 비트를 1로 설정해 Client -> Server 패킷 송신
  - 데이터 전송 (After Connection)
    - 1) Client 가 패킷 송신
    - 2) Server 에서 ACK 송신 
    - 3) Client가 ACK을 수신하지 못하면 Server로 패킷 재전송 *(신뢰성 보장)*

- **4 way-handshake**
  - Connection close
    - 1) 데이터를 전부 송신한 Client가 Client->Server로 FIN 송신
    - 2) Server가 ACK 송신
    - 3) Server에서 남은 pack 송신(일정시간 대기)
    - 4) Server가 FIN 송신
    - 5) Client가 ACK송신

- TCP 의 문제점
  - 전송의 신뢰성은 보장하지만...
    - 매번 Connection을 연결해서 시간 손실 발생
    - 패킷을 조금만 손실해도 재 전송


## UDP (User Datagram Protocol)
> **TCP 보다 신뢰성이 떨어지지만 전송속도가 일반적으로 비교적 빠른 프로토콜**  
> 순차전송 x  
> 흐름제어 x  
> 혼잡제어 x  


- Connectionless (3-handshake x)
- Error Detection
- 비교적 데이터의 신뢰성이 중요하지 않을 때 사용 (ex.영상 스트리밍)


- UDP는 tcp에서 데이터를 segment단위로 쪼갠것처럼 쪼개지 않고 전송받은 data+UDP Header 해서 User Datagram으로 데이터 처리

### UDP의 데이터 전송 방식
- Client가 SErver쪽으로 패킷 송신

## Point
> TCP, UDP 의 특성을 파악하고 상황에 따라 적절한 프로토콜을 사용  
> TCP, UDP 의 헤더에 대해 파악하고 성능 개선에 이용    
