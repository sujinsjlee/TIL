---
title: "System Design - MSA (comparison with monolithic)"
categories:
  - System Design
tags:
  - System Design
---

# MSA
![monolithic Architecture](https://www.rancher.cn/img/blog/2019/microservices-vs-monolithic-architectures/microservices-and-monolithic-architectures.jpg)  

> **Monolithic**  


- application이 구동되기위한 UI & business layer & data interface가 하나의 큰 덩어리로 같이 구성되어있는 구조

> **Microservices Architecture**


- 서비스단위를 쪼개서 구성되어있는 구조
- 서비스를 비지니스 경계에 맞게 세분화하고, 서비스간 통신은 네트워크 호출을 통해 진행하며 확장 가능하고 회복적이며 유연한 어플리케이션을 구성하는 것


##  MSA 는 왜 인기가 있을까요?
- Monolithic 방법론의 문제점은 여러기능이 뭉쳐 강하게 결합되어 있다는 점
    - 개발 유연성의 한계
    - 요구사항 대처시간 소요
    - 배포/롤백 risk
    - 리소스 낭비
    - 장애 격리/ 신뢰성

- **1** 기존 Monolithic 방식은 소프트웨어의 모든 구성요소가 한 프로젝트에 합쳐져있어, 큰 변화에 대한 대응이 어려우며, 새로운 기능 추가 및 업데이트에 어려움이 있었음
    - 반면, MSA는 **새로운 기능 추가 및 업데이트가 비교적 덜 어려움**
- **2** 기존 Monolithic 방식은  여러역할을 하는 시스템이 하나의 소프트웨어로 집합되어있어, 특정부분에 문제가 발생 시, 큰 장애로 이어질 수 있음
    - 반면 MSA는 **각각의 서비스가 분리되어있기때문에 장애가 전파되는 측면이 예방**

- **3** 기존 Monolithic 방식은 여러 역할을하는 시스템이 하나의 서버에 함께 올라가 있기에 Scale-Out시 필요없는 자원이 함께 증가됩니다.
    - 반면 MSA는 **특정 서비스에대한 Scale-out할수있어서 리소스관리측면에서 더욱 용이**

- **4 민첩하고 손쉬운 배포 및 업데이트**
    - 느슨한 결합으로 특정서비스만 업데이트하고 빌드하면되기때문에 비교적 빠르고 신규기능도입이 쉬움

## MSA 라는 아키텍처를 구성하기 위해 어떤 기술과 구성요소를 알아야할까요?

### MSA 를 구성하는 주요 Component
- **1. Config Management**
    - 환경 변수
        - 환경변수를 별도의 객체로 관리할 수 있음
    - 서비스의 재빌드, 재부팅 없이 설정사항을 반영
- **2. Service Discovery**
    - 내가 호출하고자하는 서비스에대한 ip나 포트정보, 각각의 서비스에대한 위치정보를 관리할 수 있음
- **3. API Management**
    - API에 대한 관리
    - 클라이언트 접근요청을 일원화
- **4. Centralized Logging / Tracing / Monitoring**
    - 분산화된 서비스에대한 관리 중앙집중화
- **5. Resilience & Fault Tolerance**
    - 서비스가 전체적인 장애로 이어지지않도록 실패방지구조
- **6. Auto-Scaling & Self-Healing**
    - POD 단위의 Scale-out
    - 자동 스케일링, 복구 자동화를 통한 서비스 관리 효율화

### MSA를 구현하는 기반 기술
- Spring Cloud (Java base)
- Kubernetes

### Service Mesh
- 서비스 메쉬를 사용하면 분산 마이크로 서비스 시스템을 쉽게 모니터링
- ISTIO / CONSUL

## MSA를 구축하면서 직면할 수 있는 어려움은?
- Service Mesh 적용시 고려사항
    - 복잡성 
        - 서비스 메쉬를 사용하면 런타임 인스턴스 수가 증가
    - 사이드카 컨테이너 수 증가
        - 각 서비스는 서비스 메쉬의 사이드카 프록시를 통해 호출되므로 개별 프록시 수가 증가하게 됩니다. 이에따른 부하로 서비스 운영에 문제가 발생할 가능성이 있는지에 대해 아키텍처 구조측면에서 사전에 검토해야합니다.
    - 기술력의 미성숙
        - 빠르게 발전하고 있으나 아직은 새롭고 미성숙한 기술
        - 많은 기업이 서비스 메쉬에대한 경험이 없는실정