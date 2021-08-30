---
title: "Azure 900 fundatmentals"
categories:
  - Azure
tags:
  - Azure
---


# AZ900 fundatmentals
- aka.ms/msdevkr/az900
- aka.ms/msdevkr/az900/1

# Goal
- Understand the benefits of cloud computing in Azure and how it can save you time and money
- Explain cloud concepts such as high availability, scalability, elasticity, agility, and disaster recovery
- Describe core Azure architecture components such as subscriptions, management groups, resources and resource groups
- Summarize geographic distribution concepts such as Azure regions, region pairs, and availability zones

# Introduction to Azure fundamentals
- Azure is a **cloud computing platform with an ever-expanding set of services to help you build solutions to meet your business goals.**
-  Azure services range from simple web services for hosting your business presence in the cloud to running fully virtualized computers for you to run your custom software solutions.
- Azure provides a wealth of cloud-based services like remote storage, database hosting, and centralized account management. Azure also offers new capabilities like AI and Internet of Things (IoT).

- 클라우드 컴퓨팅이란?
    - 내가 돈을 주고 컴퓨터 리소스(서버, 스토리지, 데이터베이스, 네트워킹, 소프트웨어, AI)를 사는 것
    - 다른사람이 운영하는 컴퓨터 성능 및 스토리지를 임대

- 클라우드 컴퓨팅이 일반적으로 요금이 저렴한 이유
    - 종량제 가격 책정 : 쓴만큼 돈을 낸다.
    - 운영비용 절감 : 하드웨어가 필요없으니까

- 클라우드 컴퓨팅 이점
    - 안정성 : 장애에 대한 대처
    - 확장성 : 하드웨어 사양을 높이는 수직적 scale up / 비슷한 사양의 인스턴스 추가 수평적 scale up
    - 탄력성 : resilience 트래픽이 갑자기 몰릴때 리소스 추가하여 땡겨주는등..
    - 민첩성 : 소프트웨어 자동 배포
    - 지리적배포 : 클라우드도 어딘가에 데이터센터가 물리적으로 존재하는데 지리적으로 내가 원하는 곳에서 서비스 받음
    - 재해복구 : 재해가 나더라도 백업서비스로 복구

- 클라우드 서비스 모델
    - IaaS Infrastructure as a Service
        - virtual machine
        - 가상머신에 가상네트워크를 붙여서 우리가 실제로 서버를 구성하고 거기다 app설치하고 운영 
        - 유연성 가장 높은 우리가 다해야해서
        - 단, 유지보수도 우리가 해야함

        - 서비스 제공자가 제공하는 것
            - **물리적 데이터 센터 / 건물**
            - **네트워킹 방화벽 / 보안**
            - **서버 및 스토리지**

    - PaaS Platform as a Service
        - 내가 가상머신을 운영안할래
        - 나는 코드만쓰고 배포만할래
        - 모든 것들을 클라우드 서비스들이 제공을해줌
        - virtual machine 쓰는 것보다 자유도가 떨어짐
        - 나는 몇가지 환경설정같은 것만 바꿀 수 있음
        
        - 서비스 제공자가 제공하는 것
            - 물리적 데이터 센터 / 건물
            - 네트워킹 방화벽 / 보안
            - 서버 및 스토리지
            - **운영체제**
            - **개발도구(데이터베이스관리, 비지니스분석)**

    - SaaS Software as a Service
        - 소프트웨어
        - SaaS는 코드까지 돌아가는 것
        - 사용자는 그냥 돈내고 서비스 이용하면 됩니다.
        - SaaS 같은경우는 세팅을켜고, 끄는 수준
        - SaaS 같은 경우는 소프트웨어 의존적
        - Office 365 word / ppt / excel - 클라우드에서 돌아갑니다. 이게 SaaS의 예시
        
        - 서비스 제공자가 제공하는 것
            - 물리적 데이터 센터 / 건물
            - 네트워킹 방화벽 / 보안
            - 서버 및 스토리지
            - 운영체제
            - 개발도구(데이터베이스관리, 비지니스분석)
            - **호스팅된 애플리케이션 & 앱**
    

- 서버리스 컴퓨팅
    - PaaS 에서 발전, 진화된 단계
    - 서버가 있지만 내가 관리할 서버가 없다는 것
    - PaaS 에서 scaling이라든가 instance관리를해야합니다.
    - 근데 서버리스 컴퓨팅을 쓰게되면 instance관리할 필요없음
    - 우리회사가 뭘 개발해야하는지 와관련된 핵심기능만 개발하면됩니다.

- 배포모델 : 퍼블릭, 프라이빗, 하이브리드 클라우드
    - 퍼블릭 : 누구나 클라우드의 자원을 사용 가능
    - 프라이빗 : 클라우드 자원을 나만쓰는 것
    - 하이브리드 : 퍼블릭 + 프라이빗
        - ex) 의료데이터를 실제로 저장하는 것은 private, 의료데이터를 지우고 업데이트하는 것은 퍼블릭 

    - y축 : 공유 하느냐 전용으로 쓴냐
    - x축 : 관리비용
    - 온-프레이스 : 내가 서버 관리
    - 오프프레이스 : 클라우드제공자가 관리 

- Azure 서비스
    - 이러한 서비스는 모두 몇 가지 공통적인 특성을 가지고 있습니다.
        - 중복 및 복제 기능을 갖추고 있어 내구성 과 가용성이 뛰어납니다.
        - 자동 암호화와 역할 기반 액세스 제어를 통해 보안을 유지 합니다.
        - 사실상 스토리지에 제한이 없으므로 확장성 이 뛰어납니다.
        - 유지 관리 및 사용자에 대한 중요한 문제를 관리 하고 처리합니다.
        - HTTP 또는 HTTPS를 통해 전 세계 어디에서든 액세스 할 수 있습니다.

- Azure 계정
    - https://docs.microsoft.com/ko-kr/learn/modules/intro-to-azure-fundamentals/get-started-with-azure-accounts

- 지식 점검 1:04:36
    - https://docs.microsoft.com/ko-kr/learn/modules/intro-to-azure-fundamentals/knowledge-check
    

