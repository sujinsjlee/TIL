---
title: "AWS - Preparation for Certified Solutions Architect Associate 2021"
categories:
  - AWS
tags:
  - AWS
---

# AWS Certification Challenge Program
- [AWS Certification Challenge Program](https://pages.awscloud.com/GLBL-traincert-solutions-architect-assocaite-reg-ko.html)


### 시험
- 객관식 문제, 답을 하나 또는 여러개 선택할 수 있습니다.
    - 답이 여러개인 경우, **답이 3개다 2개다** // 이런 경우가 명시되어있음 확인하고 답의 개수를 정확히 보고 고를 것
- 시험시간은 130분 + 30분(English support)
- 나중에 검토할 문항은 표시를 해둘 수 있습니다. (**Flag 버튼** 클릭)
- 어소시에이트 수준의 시험에서 필기도구는 제공되지 않습니다.
- 시험지를 제출하기에 앞서 모든 문항 또는 다시 확인하려고 표시한 문항의 답을 검토 할 수 있습니다.

### 시험고려사항
- 단일 AZ는 정답이 아닐 것이라고 예상 --> Multi - AZ에 서비스를 배포해서 고가용성을 구축하는 것을 권장
- AWS 관리형 서비스의 사용이 항상 선호됨 --> 다른회사 서비스는 답이 아닐 확률이 높음
- 내결함성(Fault Tolerance) 과 고가용성(High Availability)은 같은 개념이 아님
- 언젠가는 장애가 발생할 것으로 예상하고 이에 맞춰 설계 
- AutoScaling을 사용해야하는 시기와 이유를 파악해야합니다.
- 자신의 워크로드와 성능요구에 가장 적합한 인스턴스 및 데이터베이스 유형을 선택해야합니다.
- IAM Role은 키와 암호보다 손쉽고 안전 (**안전하게 엑세스하는~~** --> IAM Role 선택)
- 루트사용자는 사용금지
- 보안그룹(Instance 보호)은 허용만, 네트워크 ACL(subnet 보호장치)은 명시적으로 거부
- Access Keys : 유저/passwd 보다는 IAM Role(Temporary 하게 그때그때 정보를 받는 것) 을 선호
- 지속적인 사용이 예상된다면 예약인스턴스RI사용을 고려하세요
- SP savings Plan : Fargate / Lambda 에대한 할인기능이있습니다.
- 각 워크로드에 대해 가장 비용 효과적인 EC2 요금모델과 인스턴스 유형을 결정합니다.
- 사용되지 않은 CPU시간은 비용낭비입니다 --> 서버리스 (람다) 구축해야
- 가장 비용효과적인 데이터스토리지 서비스(S3 class) 및 클래스를 사용하십시오
- **배치그룹** = Placement Group 
    - Cluster / Spread / Partition
    - 어떤 배치그룹이 필요한가? 에대한 문제나옴
- **AWS Organization**
    - AWS 계정 : 루트 사용자에서 독립적으로 존재하는 단위 
    - 하나의 화사라든가 조직에서 공통의 업무를 수행하기 위해서 Multi-Account 발행
    - Multi-Account 를 중앙에서 관리하는 서비스가 AWS Organization
    - 그래서 root계정  밑에 OU (Aws Organization) 있고 OU밑에 Account달림
    - SCP : OU 통제 Service Control Policy

- **데이터베이스**
    - NoSQL : DynamoDB 
        - 성능이 초과되면 알아서 db를 추가합니다.
    - RDS 
        - **읽기성능**의 향상이 요구되면 **Read Replica** 옵션을 사용합니다.
        - 읽기성능이 부족하면 어떻게 하느냐? --> Read Replica
        - 비동기식이라 Read Replica 의 성능이 우려된다면 이에대한 해결법은?
            - **Amazon Aurora** : Read Replica 의 비동기적인 복제의 짧은 시간을 커버해줌
    - High Availability 고가용성 
        - 장애 발생시 대처와 관련된 서비스의 가용성과 관련
        - 이 경우 **Multi-AZ**로 해결
        - Master node와 stand-by node를 가까이에 두고 동기식 복제
        - 참고로, **Multi-AZ**는 읽기 성능과 관련있는게 아니라 서비스 가용성 개선을 하고자할때 해결법
    - Multi-AZ는 동기식 복제고 Read-Replica 는 비동기식 복제가 됩니다.

- **Route53 (DNS)**
    - 사용자가 물어보면 접속할 주소값을 던져줌으로써 client들이 접속할 수 있는 여러 경로에 routing option을 줍니다. option들을 하나하나 잘 체크할 것!
    - 서비스의 Health 정보체크
    - 리전간의 고가용성 보장

### Storage
- **File Storage**
    - *EFS*
        - Amazon EFS는 퍼블릭 파일을 기본적으로 지원하지 않음
    - NAS
    - 서버간에 데이터 공유
- **Block Storage**
    - *DAS or SAN* 
    - *EBS / Instance store*
    - Local 데이터 저장 및 처리
- **Object Storage**
    - *S3* : 객체를 무한대로 저장할 수 있음
    - 객체를 변경할 수 없습니다. (변경을 위해서는 객체가 교체되어야합니다.)
    - 다양한 목적 : Backup / EBS 스냅샷 / datalake / contents 배포
        - datalake : 데이터 레이크는 대규모 Raw 데이터(가공되지 않은)를 한 곳에 모아 저장하는 리포지토리

### Instance Type
- Family
- Generation
- Size
    - t3.micro *(FG.S)*

### S3 class
- S3 standard : 기본
- S3 Intelligent Tiering : 내가 사용하는 저장 비용스타일을 모르겠다싶으면 Standard / IA 알아서 정해줌
- S3 Standard - Infrequent Access (IA)  : standard 보다 저렴 
    - 파일저장등의 action이 비쌈
    - access 접근이 별로 없을때 사용
- S3 One Zone - IA : 하나의 Zone에만 저장
- S3 Glacier : 매우 저렴한 비용 지원 / 자주접근안하고 오래 보관하는 경우
    - Amazon Glacier는 퍼블릭파일을 지원하지 않음

### EBS 볼륨유형
- SSD
    - 범용 SSD
    - 프로비저닝된 IOPS SSD :관계형 DB

- HDD
    - 처리량 최적화 HDD (st1) : 로그처리
    - 콜드 HDD 

### CloudFormation
- AWS 리소스를 일관되고 재현 가능한 방식으로 배포하고 관리하기 위한 서비스
- JSON이나 YAML파일의 템플릿을 통해 생성할 리소스에대한 기본정의

### Amazon RDS 데이터베이스 엔진에 적합한 사용사례
- 복잡한 트랜잭션
- 중간 또는 높은 수준의 쿼리/쓰기 속도
    - Massive / Web-scale 쓰기속도는 --> **NoSQL** 이 적합

- RDBMS 사용자 정의 : 이건 아님 --> RDS 는 관리형으로 제공되는 서비스임. 
    - 사용자 정의로 이용하고 싶으면 EC2 에 DB 따로 설치해야

### 비관계형 데이터베이스
- Amazon Dynamo DB

### Amazon Redshift
- 관계형 데이터베이스
- Business Inteligent 환경이 꼭 필요한 DB
- 읽기 전용 복제본을 지원하지 않고 자동으로 확장하지 않음

### Amazon Aurora
- 매일 10GB 씩 증가
- 관계형 데이터베이스

### Amazon ElasticCache가 지원하는 캐시엔진
- Memchached (NoSQL)
- Redis (NoSQL)
    - SSD같은 RDS가 사용하는 데이터저장소가 아니라 in-memory 메모리에서 데이터 빠르게 처리

### AutoScaling 에대한 삼총사 서비스
- **Amazon EC2 Auto Scaling**
- **ELB : Elastic Load Balancer**
    - ASG (Autoscaling Group) 이 있음
- **CloudWatch** 
    - CloudWatch가 ASG를 watching하고 있다가 scale in / out할지 결정해서 인스턴스 추가/삭제 등을 ELB한테 알림

### Auto Scaling 특성
- Amazon EC2 인스턴스를 추가 또는 종료하여 변화하는 상황에 대응
- 지정된 AMI에서 인스턴스를 시작합니다.
- Amazone EC2 인스턴스의 최소실행갯수를 적용합니다. (min/max 값이 있음)


### CloudWatch 문제 (오답노트)
- RDS DB 인스턴스에서 CPU 사용량을 모니터링 하기 위해서 **5분씩 3번**의 기간동안 CloudWatch경보의 임계값을 70%로 설정합니다. CPU 사용량이 **10분동안 최대 80%**에 도달하면 몇 개의 경보를 받게 될 까요?
- 0개
    - 지표가 15분동안 임계값을 초과하지 않았습니다.
    - 나는 1개라고 잘못오답골랐었음.;;

### AWS KMS (Key Management Service)
- 암호화 키 관리 서비스
- 고객 키 구성 요소를 가져오도록 허용
- 키 암호화/암호 해독을 위해 애플리케이션으로부터 직접호출을 수락
- 자동으로 키를 교체하고 이전 키를 관리

### AWS CloudHSM
- 하드웨어 기반 키 관리
- 키를 안전하게 생성하고 저장

### VPC
- 사용가능한 IP address 의 region을 설정하는 것
- subnet : 각각의 AZ에 대한 주소
- 인터넷에 노출된 주소 : Public subnet
- 인터넷에 노출되지 않은 주소 : Private subnet
- NAT GW : private subnet은 Nat GW 를 통해 Internet으로 접근

### 보안그룹
- SG : 인스턴스 보안

### ACL
- 네트워크 ACL : subnet 보안

### 오답노트
- **일요일 밤마다**일괄 작업을 실행해야한다고 합시다 .이 작업은 90분내에 완료되며 **지연되면** 안됩니다. 어떤 Amazon EC2 결제 모델을 사용해야 **최상의 가격**을 확보할 수 있습니까?
    - 온디멘드 (다른옵션만큼 저렴하지 않음)
    - 예약 (작업이 실행 중이지 않을 때는 예약이 낭비일 수 있음)
    - **예정된 예약 인스턴스**
    - 스팟(작업연기가 불가능)
    