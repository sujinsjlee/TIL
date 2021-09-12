---
title: "Network - ssh"
categories:
  - Network
tags:
  - Network
---

## 원력으로 쉘을 제어 - SSH
- Secure Shell
  - 내앞에 없는 컴퓨터를 내앞에 있는 것처럼 원격으로 제어
  - Server : SSH Server 설치
  - 내 컴퓨터 (노트북): SSH Client 설치 
    - ex ) client인 나의 노트북에서 rm / ls / pwd 등의 명령어를 입력하면 이 명령어는 SSH Server 로 전달되고 명령어 결과가 SSH Client로 전달


```console
$ sudo apt-get install openssh-server
```

- 현재 리눅스에 openssh 서버를 설치하는 것

```console
$ ssh ezleesu@192.168.0.65
```

- ssh를 통해서 ezleesu@192.168.0.65 에 원격으로 접속
