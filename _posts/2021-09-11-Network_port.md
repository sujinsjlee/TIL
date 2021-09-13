---
title: "Network - port"
categories:
  - Network
tags:
  - Network
---

## Port

```console
$ ssh -p 22 ezleesu@192.168.0.65
```

- **-p** : port 옵션
- web server port : 80 port
- ssh server : 22 port

- client가 request를 할 때 해당 서버의 port로 접속

- 0 ~ 1024 port 는 well known server port // 인프라용 standard port

## Port Forwarding

> **ISP (통신사 : Internet Service Provider)** -- AP (==Router 공유기) -- 케이블 or antenna(무선) -- 노트북 / UE   
> 공유기 ip : public ip addr  
> 컴퓨터 ip : private ip addr  


- port forwarding : 라우터의 port 로 시그널이 올때 컴퓨터로 신호를 보내주는 것 

- default gateway : 공유기와 private ip주소를 가진 기기들끼리 공유하는 내부 IP

- 공유기 아이피 찾는 법

```console
$ curl httpL//ipinfo.io/
```
