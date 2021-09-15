---
title: "Network - DNS"
categories:
  - Network
tags:
  - Network
---

## DNS (Domain NameServer)

- USER가 google.com 입력 
- 컴퓨터가 DNS server 로 접속
  - DNS Server 가 google.com의 IP addr 를 알고 있음
- DNS 로부터 IP addr 를 얻으면 해당 IP addr 로 접속

- **Domain == IP**

## hosts 파일
- DNS Server가 있기 전에 각각의 컴퓨터마다 hosts file에 적혀있는 domain의 ip addr찾아서 접속

```console
$ vim /etc/hosts
```

- 참고 ) localhost 즉 내 컴퓨터의 서버 ip addr 는 127.0.0.1 
