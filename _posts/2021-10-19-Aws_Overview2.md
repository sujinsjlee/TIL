---
title: "[AWS] General Immersion Day"
categories:
  - AWS
tags:
  - AWS
---

## EC2
- Amzone Elastic Compute Cloud (EC2)
    - 서버
    - **Arm / x86 아키텍쳐** 지원
        - ARM 아키텍쳐
            - ARM 아키텍처(ARM architecture, 과거 명칭: Advanced RISC Machine, 최초 명칭: Acorn RISC Machine)는 임베디드 기기에 많이 사용되는 RISC 프로세서이다.
        - x86 아키텍쳐
            - x86은 인텔이 1978년에 개발한 인텔 8086에 적용된 아키텍처이자, 그 호환 프로세서와 후속작을 이르는 말이다. 1978년에 출시되어 40년이 지난 굉장히 오래된 아키텍처이지만, 이후에 출시된 프로세서들은 8086의 명령어 세트를 기반으로 하여 확장된 것

## Amazon EBS
- 블록스토리지
- 하나의 EBS볼륨은 하나의 인스턴스에만 연결

## EC2 인스턴스 수명 주기
- 실행중 Running
    - 인스턴스 동작중상태
    - 과금 발생
    - rebooting / stopping / shutting-down 명령으로 상태 전이 가능
- 정지됨 Stopped
    - 중지된상태
    - EBS볼륨을 루트로 사용하는 인스턴스만 가능
- 종료됨 Terminated
    - 인스턴스가 완전히 제거된 상태
    
## EC2 Instance Type
- M5d.xlarge
    - M : 인스턴스 패밀리
    - 5 : 인스턴스 세대
    - d : 추가기능
    - xlarge : 인스턴스 크기 (large 는 2 vCPU) --> xlarge는 4vCPU

- EC2 인스턴스 추가기능 
    - g : *AWS Graviton 프로세서*
    - a : AMD EPYC 프로세서
    - d : 빠른 로컬 NVMe 스토리지
    - n : 최대 100Gbps 네트워크 성능
    - e : Enhanced performance

## EC2 구매 옵션
- **온디맨드** : 초단위로 컴퓨팅 용량 지불
- **RI** : 예약인스턴스 1년/3년 약정으로 온디맨드 가격에서 대폭 할인
- **스팟인스턴스** : 인스턴스의 가격이 주가처럼 가변적인 인스턴스 가격정책
- **세이빙플랜** : EC2 및 Fargate/lambda 에 대해 저렴한 요금을 제공하는 유연한 요금 모델

## 비용최적화 (시험에 나온적있음)
> 유연하고 내결함서을 갖춘 워크로드 --> **스팟인스턴스**  
> 급증하는 Stateful 워크로드의 스케일링 --> **온디멘드 인스턴스**  
> 장기적으로 사용하는 안정적인 워크로드 -->  **예약인스턴스 또는 세이빙 플랜**으로 비용 절감  

## ELB 
- ALB Application Load Balancer
    - Layer7
- NLB Network Load Balancer
    - Layer4

## AWS CloudWatch 
- AWS 리소스 및 애플리케이션의 모니터링

## AWS Systems Manager(Systems Manager로 뭘 하는지..가 시험에 자주나옴)
- 패치 및 구성의 준수 유지
- 여러 계정 및 지역에서 자동화
- 브라우저 및 CLI를 통해 Amazon EC2 인스턴스에 연결
- 여러 계정에서 소프트웨어 인벤토리 추적
- 속도 제어를 통해 인스턴스에 에이전트를 안전하게 설치

## Amazon RDS
- Amazon 관계형 데이터베이스
- Relational Database
- Aurora / MySQL / MariaDB / ORACLE / PostgreSQL

## DB 가용성 및 내구성 - Multi AZ
- 물리적으로 분리된 가용영역에 *standby* 데이터베이스를 운영하여 가용성을 높임
- 동기식 복제 - 높은 내구성
- primary / secondary DB 구성
- 자동 Failover(1~2분이내)

## DB 가용성 및 내구성 - 읽기전용 복제본
- 읽기업무를 분담하여 소스 데이터베이스에대한 워크로드 부하 완화
- 비동기식복제 - 높은 가용성

## Aurora
- AWS 역사상 가장 빠르게 성장하는 서비스
- 확장, 분산형 아키텍쳐
- Amazon Aurora는 내결함성을 갖춘 자가 복구 분산 스토리지 시스템으로, 데이터베이스 인스턴스당 최대 128TB까지 자동으로 확장됩니다. 대기 시간이 짧은 읽기 전용 복제본 최대 15개, 특정 시점으로 복구, Amazon S3로 지속적 백업, 3개 가용 영역에 걸친 복제를 통해 뛰어난 성능과 가용성을 제공

- [Amazon Aurora: Design Considerations for High Throughput Cloud-Native Relational Databases](https://www.allthingsdistributed.com/files/p1041-verbitski.pdf)
- Read Replica
- [Aurora faqs](https://aws.amazon.com/ko/rds/aurora/faqs/)

## Amazon Redshift
- 빠르고 강력한 페타바이트 규모의, 데이터 웨어하우스

## Amazon DynamoDB
- 어떤 규모에서도 10밀리초 미만의 성능을 제공
- 사실상 무제한의 처리량과 스토리지
- 초당 2000만개 이상의 피크요청을 지원 가능

## Amazon DocumentDB
- MongoDB 호환

## AWS 데이터베이스 마이그레이션 서비스 (DMS)
- 관리형 데이터 마이그레이션 서비스
- 동종 및 이기종 데이터 복제 지원 --> 100% 복제되는 것은 아니지만 지원
    - RDBS -> NRDBS
    - NRDBS -> RDBS
- **SCT** : 기존 데이터베이스스키마를 다른 데이터베이스 엔진스키마로 변환
    - *Schema Conversion Tool*
    