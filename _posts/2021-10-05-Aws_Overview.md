---
title: "AWS - General Overview"
categories:
  - AWS
tags:
  - AWS
---

# AWS Network - General Immersion Day

## AWS VPC Overview
- Virtual Private Cloud
    - 가용영역 : 물리적 데이터 센터 지역
    - 물리적은 아니지만 가상으로 쪼개놓은 네트워크 공간
    - IP범위 조절가능
    - Subnet 세팅 가능 
    - Routing table 세팅 가능
    - elastic IP : 고정 IP --> elastic IP관련해서 쿼터제 있음
        - 고객 : 서버100대 띄우고싶은데 100대 안띄어져
        - 왜냐면 elastic IP 는 쿼터제가 있고 EC2 는 인스턴스 만드는데 시간이 걸리기 때문
    - public IP : 계속 변환되는 IP

## AWS VPC 생성순서
- 리전 선택 및 IP주소 범위설정
- 인터넷 게이트웨이 생성 : 인터넷 게이트웨이는 VPC하나만 할당이 됩니다.
- 가용영역내에 필요한 서브넷 정의
- 라우팅 구성
- VPC 로 송수신되는 트래픽제어


## CIDR --> 면접에서도 많이 나옴
- https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Subnets.html  
- [CIDR 서브넷 공부](https://www.youtube.com/watch?v=aVTEZHC2wdA)  

## 온프레미스(On-premises)
소프트웨어 등 솔루션을 클라우드 같이 원격 환경이 아닌 자체적으로 보유한 전산실 서버에 직접 설치해 운영하는 방식
- 오프프레미스(Off-premises)
오프프레미스란 일반적으로 SaaS 또는 클라우드 컴퓨팅이라고 한다. 온프레미스의 반대로 인터넷 네트워크에 연결된 서버팜이나 클라우드의 원격 실행환경을 의미

온프레미스와 오프프레미스의 가장 큰 차이점은 바로 기업내 구축형으로 사용하느냐, 클라우드 기반의 임대 서비스를 사용하느냐 이다.

## (참고) 주소범위 CIDR 이해하기
- #of hosts (EC2 개수)

## 네트워크 Access Control List / Security Group 차이점 암기
- 네트워크 ACL
    - Stateless 방화벽
    - 서브넷 대상 경계의 방화벽
- 보안 그룹
    - Stateful 방화벽
    - AWS 리소스(대상)에 대한 방화벽

## VPC peering 구성전에 알아두어야할 것들
- 같은 리전의 VPC Peer에서 Security Group 참조가능
- DNS Host Name을 참조해서, Private IP주소 반환 가능
- IPv4/v6 주소 모두 Peering 가능
- **IP 주소 대역 중복할당 불가능**
- **양방향 Peering 불가능**
- **VPC Peering 에서 Jumbo Frame 사용 불가능**


## Useful Links
- edx :
  - [AWS Cloud Technical Essentials](https://www.edx.org/course/aws-cloud-technical-essentials)
  - [Introduction to AWS Identity and Access Management](https://www.edx.org/course/introduction-to-aws-identity-and-access-management)
- aws training :
  - [Exam Readiness: AWS Certified Solutions Architect – Associate (Digital)](https://www.aws.training/Details/Curriculum?id=20685)


