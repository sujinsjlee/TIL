---
title: "Network - Server and Webserver"
categories:
  - Network
tags:
  - Network
---


# server
> **server** : client로 부터 request를  받고 response를 줌  
> **client** : server로 request를 요청  

# domain
> google.com (domain name)  

# ip address

```console
$ ping google.com
```

- google.com 입력 > DNS 서버에서 DB를 뒤져서 domain name과 맞는 ip주소 반환 > request 된 ip주소로 연결

- 현재 컴퓨터의 ip알아내는 법

```console
$ ip addr 
```
- inet 이후가 자신의 컴퓨터 ip address
- [웹사이트검색](ipinfo.io/ip)
    - 위의 두개의 조회 결과가 같을 수도 다를 수 도있음
    - ip addr : 컴퓨터에 실제 ip --> 공유기에 개별적으로 연결된 private ip (사설 IP == private address)
    - 웹사이트 검색 : 공유기 (==Access Point==Router) 의 public ip (공인 IP == public Address)


# webserver

- Web Browser : firefox / Chrome
- **Web Server : Apache / nginx / IIS**

- **local host** :  웹브라우저입장에서 자신의 서버 컴퓨터의 웹서버에 접속할때 사용하는 주소는 **local host (==127.0.0.1)**

# configuration
- 어떤 프로그램이 어떻게 동작할 것인가
  - **/etc** : 유닉스계열에서는 /etc로 들어가면 확인 가능
    - ~~~.conf 파일이 설정파일

- server 프로그램의 에러원인을 찾고싶을 때 해당 프로그램에서 error.log / access.log 파일 활용