---
title: "Docker (1) - Concept"
categories:
  - Docker
tags:
  - Docker
link: //
publish: false
---

# Docker

## Docker Concept
- 가상 머신(**Virtual Machine**): 컴퓨터 안에 또 다른 컴퓨터를 동작 시키는 것  
    - **실제로 machine은 하나인데 virtual 로 쪼개서 쓰는 것**
    - VM은 OS를 만드는 것  
    - **OS** (Operating System) - ex : window, mac, Linux
    - OS 밑에는 하드웨어(monitor, pc)가 있고 그 HW 를 운영하기 쉽게 해주는 것이 OS
    - **Docker**는 linux container에서 온 Process
    - A virtual machine (VM) is a virtual environment that functions as a virtual computer system with its own CPU, memory, network interface, and storage, created on a physical hardware system (located off- or on-premises).
    - A virtual machine is a program that acts as a virtual computer. It runs on your current operating system (the host operating system) and provides virtual hardware to guest operating systems. The guest OS runs in a window on your host OS, just like any other program on your computer.

### BackGround
**Software(Application) Engineer**  
    - S/W Application - 서버개발자 / 클라이언트 개발자로 나누어짐

**System(Infra) Engineer**  
    - H/W, Network, OS, Middleware
    - 하드웨어를 주로 다룸
    - 네트워크 장비깔고..선도 설치하고..하는등의 업무

**On-Premises**
    - 아마존이나 구글 서버를 쓰는 것이아니라
    - 우리회사만의 서버가 자체적으로 있는 것(*IntraNet*)
        - Intra Net 을 쓰는 경우

**Cloud Platform**  
    - AWS, GCP, KT, etc

**Orchestration**  
