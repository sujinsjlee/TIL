---
title: "Network - Internet"
categories:
  - Network
tags:
  - Network
---

## IP 
> **IP주소** : Internet Protocol Address    
> 인터넷 체계가 동작하기 위해서 이 체계위에 접속하는 컴퓨터/통신장비가 각자 지켜야하는 준수해야할 protocol이 있음  


- 인터넷에 연결된 각각의 컴퓨터는 서로 정보를 주고받기 위해서 **주소**가 필요함 --> **IP주소**

- IP주소 확인
    - Window 
        - Window + R key : ping ~~~.com
    - Mac
        - Terminal : ping ~~~.com
    - Linux
        - ping ~~~.com

- 통신을 하기 위해서는 서버 + 클라이언트 모두 IP 주소를 알고 있어야함
- 검색엔진에서 myip 검색



## DNS Domain Name System
> IP 주소 --> Domain name   
> **Domain** : IP주소에 대응되는 이름  


- 사실 컴퓨터는 도메인을 통해서 서버에 접속 x
- 실제로 컴퓨터가 동작할때는 서버에 접속하는 것은 IP주소를 통해서만


> **Name Server**  


- 클라이언트컴퓨터는 Name Server 에 접속을 해서 Domain의 Ip주소를 request 
- Name Server : 각각의 Domain 과 Ip주소 관계를 저장


## IPv6
> **IPv6** : IP 주소 부족 고갈 문제에대한 해결방안  


- 기존의 IPv4 주소체계
    - **0.0.0.0 ~ 255.255.255.255**
    - 42억개의 IP주소체계

- IPv6 : 2의 128승

## Port
- **Port Forwarding**
    - 공유기는 공유기의 IP주소인 공인 IP주소가 있음
    - 공인 IP로 클라이언트가 접속했을 때 공유기는 IP 주소를 공유기와 연결된 사설IP(웹서버 IP)로 토스
    - http//222.109.62.43:80 == 80번 포트의 소프트웨어에 접속하겠다
        - **:80** 
        - 80번 포트 : 웹서버
    - **:8080** - 8080 포트역시 웹서버 포트

## 와이파이(Wi-fi)란?
- Wi-Fi
와이파이란 Wireless fidelity의 약자로, IEEE 802.11 통신규정을 만족하는 기기들끼리 무선으로 데이터를 주고받을 수 있도록 하는 기술을 뜻한다. IEEE 802.11은 미국전기전자학회 (IEEE)에서 개발한 무선 랜 규격이다.

와이파이를 사용하려면 무선 접속 장치(AP: Access point)가 있어야 한다. 우리는 흔히 이 AP를 ‘공유기’라 부른다. 흔히 집이나 사무실 등, ‘랜선’을 이용해 인터넷을 사용할 때 이를 유선인터넷이라 부른다.

공유기를 설치하면 이 유선인터넷 회선에 흐르는 인터넷 신호를 무선 신호로 바꿔주어 신호가 닿는 범위 내에서 랜선을 연결하지 않고도 ‘무선’ 인터넷을 사용할 수 있는 것, 이것이 와이파이다. 공유기의 성능에 따라 와이파이를 사용할 수 있는 범위가 정해지고, 이 범위를 벗어나면 신호 강도가 약해져 와이파이를 사용할 수 없다.

- Wifi 
    - Wifi : Wireless fidelity 
    - Wireless signal from AP
    - AP is connected to router and modem
    - AP sending wireless signal 

## 이동통신 mobile telecommunication
- **LTE**는 이동통신에서 출발한 것이 핵심
- 이동통신은 장소에 구애받지 않고 이동 중에도 전화를 하기위해 탄생한 기술
- Since LTE is accessed through a mobile device, its range is virtually limitless.

It can be confusing how some devices, like your phone, always seem to be connected to the internet and other devices, like a tablet, are only connected at home or where there is public Wi-Fi.

Your computer and usually a tablet (unless you purchased it through your cell phone company), only connects to Wi-Fi. Some desktop computers may not even connect to Wi-Fi and need to be hardwired to the Ethernet cable (which connects to the router).

Your phone connects to WiFi and LTE (Long Term Evolution). While Wi-Fi comes from your cable and internet provider, LTE is a wireless broadband sent through the radio spectrum. To access LTE, you pay your cell phone provider. You most likely pay a monthly bill for different data caps of usage. 
