---
title: "AWS - Ultimate AWS Certified Solutions Architect Associate 2021"
categories:
  - AWS
tags:
  - AWS
---


# Udemy - Ultimate AWS Certified Solutions Architect Associate 2021
> [Section3 Getting started with AWS](#section3)  
> [Section4 IAM & AWS CLI](#section4)  
> [Section5 EC2 Fundamentals](#section5)  
> [Section6 EC2 Solution Architect Associate Level](#section6)  
> [Section7 EC2 Instance Storage](#section7)  
> [Section8 High Availability and Scalability:ELB & ASG](#section8)  
> [Section9 AWS Fundamentals: RDS + Aurora + ElasticCache](#section9)  
> [Section10 Route53](#section10)  
> [Section11 Classic Solutions Architecture Discussions](#section11)  
> [Section12 Amazon S3 Introduction](#section12)  
> [Section13 AWS SDK, IAM Roles & Policies](#section13)    
> [Section14 Advanced Amazon S3 & Athena](#section14)    
> [Section15 CloudFont & AWS Global Accelerator](#section15)    
> [Section16 AWS Storage Extras](#section16)   
> [Section17 Decoupling applications: SQS, SNS, Kinesis, Active MQ](#section17)  
> [Section18 Containers on AWS: ECS, Fargate, ECR & EKS](#section18)  
> [Section19 Serverless Overviews from a Solution Architect Perspective](#section19)  
> [Section20 Serverless Solution Architecture Discussions](#section20)  
> [Section21 Database in AWS](#section21)  
> [Section22 Monitoring & Audit:CloudWatch, CloudTrail & Config](#section22)  
> [Section23 IAM - Advanced](#section23)  
> [Section24 AWS Security & Encryption: KMS, SSM Parameter Store, CloudHSM, Shield, WAF](#section24)  
> [Section25 Networking - VPC](#section25)  
> [Section26 Disaster Recovery & Migrations](#section26)  
> [Section27 More Solution Architectures](#section27)  
> [Section28 Other Services](#section28)  
> [Test](#Practice_Exam)






## section3
### Getting started with AWS  
- **AWS Regions** is a cluster of data centers
- How to choose an AWS Region
  - **Compliance** with data governance and legal requirements: data never leaves a region without  your explicit permission
  - **Proximity** to customers: reduced latency
  - **Available** services within a Region: new services and new features aren’t available in every Region
  - **Pricing**: pricing varies region to region and is transparent in the service pricing page
- AZ
  - Each region has many availability zones(usually 3, min is 2, max is 6).
  - Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity
  - They’re separate from each other, so that they’re isolated from disasters

## section4
### IAM & AWS CLI  
- IAM = Ideneity and Access Management, Global
  - Users are people within your organization, and can be grouped
  - **Groups only contain users, not other groups**
  - Users don’t have to belong to a group, and user can belong to multiple groups

- IAM Policy
  - IAM Permission
  - Users or Groups can be assigned JSON documents called policies
  - Inline policy : an inline policy which has a policy that's only attached to one user.

- ARN
  - Amazon 리소스 이름(ARN)은 AWS 리소스를 고유하게 식별합니다. 모든 전반에 리소스를 명료 하게 지정해야 하는 경우 ARN 이 필요합니다.AWS에서 IAM 정책, Amazon RDS (Amazon Realtional Database Service) 태그 및 API 호출과 같은 서비스를 제공합니다.

- 퀴즈 1: IAM & AWS CLI Quiz
  - An IAM policy consists of one or more statements. A statement in an IAM Policy consists of the following
    - Sid
    - Effect
    - Principle
    - Action
    - Resource
  - According to the AWS Shared Responsibility Model, which of the following is AWS responsibility?
    - AWS Infrastructure
    - Configuration and vulnerability analysis
    - Compliance validation
    
## section5
### EC2

- EC2 Bootstrap
  - It is possible to bootstrap our instances using an EC2 User data script
  - 부트스트랩은 EC2 인스턴스를 AWS가 내부적으로 생성하면서 초기에 EC2가 수행할 명령을 미리 지정하는 것을 의미
  - 주로 운영체제의 패치/모듈의 설치 혹은 업데이트를 진행할때 사용
  - 관리콘솔 -> EC2 설정 -> Configure Instance Details -> Advance Details > User Data
  - UserData 에 text로 입력하는 내용
    - 첫 라인은 #!/bin/bash
    - 그 아래 라인부터 각종 패키지  설치, 기존 패키지 업데이트, 서비스 시작할 데몬 등

    ```js
    #!/bin/bash
    aws s3 sp s3://myInternalBucket/myfilefolder/myfile.jar /myfolder
    ```

- Classic Ports
  - 22 = SSH(Secure Shell) : log into a Linux instance
  - 21 = FTP(File Transfer Potocol) : upload files into a file share
  - 22 = SFTP(Secure File Transfer Protocol) : upload files using SSH
  - 80 = HTTP : access unsecured website
  - 443 = HTTPS : access secured website
  - 3389 = RDP (Remote Desktop Protocol) : log into a Windows instance

- SSH
  - SSH
    - SSH란 Secure Sell의 약자이다. 원격지의 컴퓨터. 즉 멀리 떨어져있는 컴퓨터. 내 컴퓨터가 SSH 클라이언트, 원격에 있는 컴퓨터를 SSH Server라고 부른다. 이것은 Shell로 접근이 가능하고 제어가 가능하다 SSH는 통신 프로토콜이다. 이러한 것들을 SSH라고 부른다. Secure가 붙은 이유는 안전하기 때문이다. 
    - 리눅스와 MAC과 같은 유닉스 계열에서는 SSH 서버와 SSH 클라이언트를 모두 내장하고 있지만, 윈도우의 경우에는 유닉스 계열의 컴퓨터를 제어하기 위해 프로그램 설치가 필요하다. 이 때 쓰이는 프로그램이 Putty
    - [생활코딩 SSH](https://opentutorials.org/module/432/3738)

- 퀴즈 2 : EC2 Fundamentals Quiz
  - How long can you reserve an EC2 Reserved Instance?
    - EC2 Reserved Instances can be reserved for 1 or 3 years only.
  
  - Which EC2 Instance Type should you choose for a critical application that uses an in-memory database?
    - Memory Optimized EC2 instances are great for workloads requiring large data sets in memory.
  
  - You have an e-commerce application with an OLTP database hosted on-premises. This application has popularity which results in its database has thousands of requests per second. You want to migrate the database to an EC2 instance. Which EC2 Instance Type should you choose to handle this high-frequency OLTP database?
    - Storage Optimized

## section6
### EC2
- Placement Groups
  - Cluster
  - Spread
  - Partition
    - EC2 instances get access to the partition information as metadata
    - *metadata* : Contrtucted data with purpose (Metadata is "data that provides information about other data", but not the content of the data, such as the text of a message or the image itself.)

- ENI (Elastic Network Interfaces)
  - Elastic Network Interface(이 문서에서는 네트워크 인터페이스로 표시)는 VPC에서 가상 네트워크 카드를 나타내는 논리적 네트워킹 구성 요소
  - [ENI Concept - AWS officials](https://aws.amazon.com/ko/blogs/aws/new-elastic-network-interfaces-in-the-virtual-private-cloud/)

## section7
### EBS & EFS
- **Elastic Block Storage**
  - network volume that should be mounted only on one instance and locked to an AZ
- **EC2 Instance Store** (attache directly EC2 with physical connection)
  - to get the mamximum amount of IO onto an EC2 instance
  - ephemeral drive
- **Elastic File System**
  - network file system to be mounted across multiple AZs

- **POSIX**
  - *Portable operating system interface*
  - 서로 다른 UNIX OS의 공통 API를 정리하여 이식성이 높은 유닉스 응용 프로그램을 개발하기 위한 목적으로 IEEE가 책정한 애플리케이션 인터페이스 규격
  - POSIX는 운영체제 자체가 아니라 응용 프로그램과 운영체제 간의 ‘인터페이스’를 정의하는 개념이기 때문에 프로그래머는 인터페이스가 존중되는 한 운영체제와 응용 프로그램을 자유롭게 작성


## section8
### ELB
- Application LB
  - Load Balancing to multiple applications 
  - A great fit for micro services & container-based application
  - fixed hostname

- Network LB
  - one static IP per AZ
  - Forward TCP & UDP traffic to your instances

- SSL & TLS
  - SSL과 TLS는 모두 웹 서버와 사용자의 웹 브라우저 간 통신을 암호화 하는데 사용되는 프로토콜입니다. 공개 키와 개인 키를 교환하여 보안 세션을 생성하여 통신을 암호화하는 방식을 사용합니다. TLS는 MAC 함수 생성을 위해 다른 암호화 알고리즘을 사용하며, 이는 이전 버전의 SSL보다 많은 경고 코드를 포함하고 있습니다.

- SNI(Server Name Indication)
  - SNI solves the problem of loading multiple SSL certificate onto one web server (to serve multiple servers)
  - TLS 프로토콜 확장형이고 랜선을 통하여 tcp 통신을 수행할 시에 핸드세이크 과정을 거치게 되는데, 이때 핸드세이크 과정의 시작점에서 웹브라우저에게 호스트명을 정해줍니다. 이 방식을 통하여 동일서버에서 여러개의 SSL 통신이 가능하게 됩니다.
  - TLS는 HTTP 아래 단계인 전송 레이어에 속하기 때문에 클라이언트가 요청하는 호스트 이름을 알지 못합니다. 이때 클라이언트가 처음 연결 시 서버에게 “이것이 내가 인증서를 원하는 도메인입니다”라고 지정할 수 있도록 도와주는 것이 바로 SNI입니다. 그러면 서버가 올바른 인증서를 선택하여 클라이언트에게 응답할 수 있습니다. 오늘날 모든 웹 브라우저와 대다수 클라이언트는 SNI를 지원합니다. 실제로 CloudFront에 연결되는 클라이언트의 99.5% 이상이 SNI를 지원하고 있습니다.

- Connection Draining
  - *ELB Connection Draining – Remove Instances From Service With Care*
  - Auto Scaling이 사용자의 요청을 처리 중인 EC2 인스턴스를 바로 삭제하지 못하도록 방지하는 기능입니다. 
  - 예를 들어 사용자 수가 줄어들면 Auto Scaling이 EC2 인스턴스를 삭제합니다. 마침 사용자가 해당 EC2 인스턴스에서 파일을 다운로드하고 있었는데 EC2 인스턴스가 삭제되어버리면 파일 다운로드는 중간에 끊어집니다. EC2 인스턴스를 삭제하기 전에 사용자의 요청을 처리할 수 있도록 지정한 시간만큼 기다립니다. 그리고 기다리는 동안에는 새로운 커넥션을 받지 않습니다
  - When Connection Draining is enabled and configured, the process of deregistering an instance from an Elastic Load Balancer gains an additional step. For the duration of the configured timeout, the load balancer will allow existing, in-flight requests made to an instance to complete, but it will not send any new requests to the instance.

## section9
### DB
- Stateless란 http와 같이 client의 이전 상태를 기록하지 않는 접속이란 의미입니다. 그에 비해 Stateful은 client의 이전 상태를 기록하고 있는 것이죠.
- Stateless는 웹서버가 사용자의 작업을 기억하고 있지 않다는 의미이고 Stateful은 사용자의 상태를 서버가 기억하고 있다가 유용한 정보로써 활용한다는 것입니다.

> Here's a list of standard ports you should see at least once. You shouldn't remember them (the exam will not test you on that), but you should be able to differentiate between an Important (HTTPS - port 443) and a database port (PostgreSQL - port 5432) 



- **Important ports**

  - FTP: 21
  - SSH: 22
  - SFTP: 22 (same as SSH)
  - HTTP: 80
  - HTTPS: 443

- **RDS Databases ports**

  - PostgreSQL: 5432
  - MySQL: 3306
  - Oracle RDS: 1521
  - MSSQL Server: 1433
  - MariaDB: 3306 (same as MySQL)
  - Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)

## section10
- **Routing Policies Latency-based vs. Geolocation**
  - Latency-based routing policy does ensure that the user will have a good experience in terms of latency. However, latency based routing does not always ensure that the traffic is routed to the nearest resource in terms of proximity to the source of the query.

  - For latency-based routing, you create latency records for your resources in multiple AWS Regions. When a DNS query is received by Route 53 for your domain or sub-domain, it evaluates the latency records that you have created for AWS Regions. Then, it will determine which region provides the lowest latency to the user, and then selects the appropriate latency record for that region.

  - However, latency will not remain same all the time. It can change as the network connectivity, traffic and routing change over time. Latency-based routing works according to the latency measurements over a period of time, and the changes are revealed in the measurements. So in this case, the latency routing policy will not work since the routing changes over time.

  - Now let us look at the Geolocation routing. It allows Route 53 to route the traffic to the resources according to the geographic location of the source query. You can make your content localized and display your website in your own language in the Geolocation routing.

  - A use case for Geolocation routing:
    - *If you’ve country-specific distribution rights you can control the content distribution to a specific country.*
  - With Geolocation routing policy all the criteria mentioned in the scenario is satisfied. Hence, a user from Lille will be directed to a resource in the Paris region, similarly a user in Bristol will be directed to London region and a person in California will be directed to US West region and the user data will be stored in the appropriate servers located in that region. So here using Geolocation routing policy will also ensure that the person from Lille will view the website and contents in French, a user from Bristol will view it in English. 
  - It is important to note that Geolocation route policy maps IP addresses to locations while working. However, some IP addresses aren’t mapped to geographic locations. In such cases, Route 53 returns a “no answer” response for queries from those locations unless the default record is created. And when a default record is created, it will handle the queries from IP addresses that are not mapped to any location

- **ELB vs. Multi-Value**
  - [ELB vs. Routing 53 Policies(Multi-Value)](https://acloud.guru/forums/aws-certified-solutions-architect-associate/discussion/-KTWtu_Y5HscAAS8NCyc/elb-vs-route-53-routing)
  - In summary, I believe ELBs are intended to load balance across EC2 instances in a **single** region. Whereas DNS load-balancing (Route 53) is intended to help balance traffic **across** regions. Route53 policies like geolocation may help direct traffic to preferred regions, then ELBs route between instances within one region.

  - Functionally, another difference is that DNS-based routing (e.g. Route 53) only changes the address that your clients' requests resolve to. On the other hand, an ELB actually reroutes traffic.

  - One analogy is: if you ask for the closest WalMart, you may get an address based on your location, but you could choose to go to another Walmart if you know one. That's Route 53; it just switches the address resolved based on some context. On the other hand, a policeman redirecting traffic because of construction, is more like an ELB, he/she is actually changing the traffic flow, not just suggesting.

- 퀴즈 오답
  - **CNAME vs. Alias 비교**
    - You can't create a CNAME record that has the same name as the top node of the DNS namespace (Zone Apex), in our case "mycoolcompany.com."

## section11
- **A cache hit** is a state in which data requested for processing by a component or application is found in the cache memory. 

- **Golden AMI** is an image that contains all your software installed and configured so that future EC2 instances can boot up quickly from that AMI.

- Golden AMI is an image that contains all your software, dependencies, and configurations, so that future EC2 instances can boot up quickly from that AMI.

- Which of the following will NOT help us while designing a STATELESS application tier? 다음 중 STATELESS 애플리케이션 계층을 설계할 때 도움이 되지 않는 것은 무엇입니까?

## section12
-  an IAM principal can access an S3 object if 
  - the user IAM permissions allow it OR the resource policy ALLOWS it
  - AND there’s no explicit DENY
- **Explicit DENY in an IAM Policy will take precedence over an S3 bucket policy.**

- **CORS**
  - Cross-Origin Resource Sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. 
  - [To learn more about CORS](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html)


## section13
- **curl**
  - http를 이용하여 경로의 데이터를 가져온다.
  - `curl [옵션][url]`

- **Versioning**
  - S3는 특정 버킷의 객체들에 대하여 버전 관리 기능을 하는 버저닝 기능을 제공한다. 버저닝 기능을 사용하면 파일을 삭제 후 복원할 수 있고 이전으로 되돌릴 수도 있다. 하지만 버저닝 되는 객체도 그만큼 S3의 용량을 차지한다. 
  - 버저닝은 Suspend도 가능한데 Enable된 상태에서 Versioning을 보면 Enable이 Suspend로 바뀌어 있는 것을 볼 수 있다. Suspend 상태에서 파일을 바꾸면 Version ID가 null이 되며 이 상태로 복원할 수 없다.

## section14
- Multi-Part-upload
  - [멀티파트 업로드 (KR)](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/mpuoverview.html)
  - [Multipart upload (EN)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html)
  - 멀티파트 업로드를 사용하면 단일 객체를 여러 파트의 집합으로 업로드할 수 있습니다. 각 파트는 객체 데이터의 연속적인 부분입니다. 이러한 객체 파트는 독립적으로 그리고 임의의 순서로 업로드할 수 있습니다. 파트의 전송이 실패할 경우 다른 파트에 영향을 주지 않고도 해당 파트를 재전송할 수 있습니다. 객체의 모든 파트가 업로드되면 Amazon S3가 이들 파트를 수집하여 객체를 생성합니다. 일반적으로 객체 크기가 100MB에 근접할 경우, 단일 작업에서 객체를 업로드하는 대신 멀티파트 업로드 사용을 고려해 봐야 합니다.
  - 부분을 업로드할 때 업로드 ID와 함께 부분 번호를 지정해야 합니다. 1부터 10,000까지 부분 번호를 지정할 수 있습니다. 부분 번호를 사용하여 업로드하는 객체에서 각 부분과 그 위치를 고유하게 식별합니다. 부분 번호는 굳이 연속 시퀀스로 선택할 필요가 없습니다(예를 들면 1, 5 및 14를 선택해도 됩니다). 이전에 업로드한 부분과 동일한 부분 번호로 새 부분을 업로드할 경우 이전에 업로드한 부분을 덮어쓰게 됩니다.

## section15
- **CDN**
  - CDN이란? Content Delivery Network의 약자인 CDN은 지리적 제약 없이 전 세계 사용자에게 빠르고 안전하게 콘텐츠를 전송할 수 있는 콘텐츠 전송 기술을 의미
  - CDN은 서버와 사용자 사이의 물리적인 거리를 줄여 콘텐츠 로딩에 소요되는 시간을 최소화
  - CDN은 각 지역에 캐시 서버(PoP, Points of presence)를 분산 배치해, 근접한 사용자의 요청에 원본 서버가 아닌 캐시 서버가 콘텐츠를 전달
  - 예를 들어 미국에 있는 사용자가 한국에 호스팅 된 웹 사이트에 접근하는 경우 미국에 위치한 PoP 서버에서 웹사이트 콘텐츠를 사용자에게 전송하는 방식

- CDN이 필요한 경우

  - 인터넷을 통해 비즈니스를 운영하거나 웹 사이트에서 그래픽 이미지, 동영상 파일 등의 콘텐츠를 제공한다면 CDN 서비스를 이용할 필요가 있습니다. CDN은 동영상 스트리밍이나 온라인 게임, 대용량 파일 전송, 그리고 해상도가 높아 용량이 큰 이미지를 다루는 쇼핑몰, 포털 사이트 등에서 안정적인 서비스 제공을 위해 활용되고 있습니다.

  - 하지만 특정 국가나 지역만을 타깃으로 하는 웹 서비스를 운영한다면 CDN 서비스를 활용할 필요가 없습니다. 이 경우 CDN을 이용하면 오히려 불필요한 연결 지점이 늘어나 웹 사이트의 성능 저하를 불러올 수 있기 때문입니다.

- **Hop**
  - In wired computer networking, including the Internet, a hop occurs when a packet is passed from one network segment to the next.
  - Data packets pass through routers as they travel between source and destination. The hop count refers to the number of network devices through which data passes from source to destination
  - 출발지와 목적지 사이에 위치한 경로내에서 그 양끝단을 포함할 모든 네트워크 장비중 다음 네트워크 장비로 패킷이 이동할때마다의 이동

- 다음 홉 (Next Hop)
  - 목적지 네트워크까지 가기위한 바로 다음의 라우터를 말함

- 홉 수 Hop Count
  - 거치게 되는 라우터수

- **Q: AWS Global Accelerator와 Amazon CloudFront의 차이점**
  - [FaQ](https://aws.amazon.com/ko/global-accelerator/faqs/)
  - A: Global Accelerator 및 Amazon CloudFront는 AWS 글로벌 네트워크와 전 세계에 분포된 해당 엣지 로케이션을 사용하는 별도의 두 서비스입니다. CloudFront는 캐시 가능한 콘텐츠(예: 이미지, 비디오)와 동적인 콘텐츠(예: API 가속화 및 동적 사이트 제공)의 성능을 모두 개선합니다. Global Accelerator는 엣지에서 패킷을 단일 또는 여러 AWS 리전에서 실행되는 애플리케이션으로 프록시하여 TCP 또는 UDP를 통해 광범위한 애플리케이션의 성능을 개선합니다. Global Accelerator는 게임(UDP), IoT(MQTT) 또는 VoIP와 같은 HTTP 외 사용 사례는 물론, 특별히 정적 IP 주소 또는 결정적 빠른 지역 장애 복구를 요구하는 HTTP 사용 사례에 적합합니다. 두 서비스 모두 DDoS 공격을 막기 위해 AWS Shield와 통합되어 있습니다.

## section16
- **AWS Snow Family**
  - The AWS Snow Family is a service that helps customers who need to run operations in austere, non-data center environments, and in locations where there's no consistent network connectivity. You can use these devices to locally and cost-effectively access the storage and compute power of the AWS Cloud in places where an internet connection might not be an option.

- **FTP**
  - FTP란 파일 전송 프로토콜(File Transfer Protocol)의 약자입니다. 그 의미를 자세히 살펴봅시다. 기본적으로 '프로토콜'은 전자기기가 서로 통신하는 데 필요한 절차나 규칙을 뜻하죠. FTP는 TCP/IP 네트워크(인터넷)상의 장치가 파일을 전송할 때 사용하는 규칙입니다. 인터넷을 사용할 때 우리는 다양한 프로토콜을 사용합니다. 인터넷을 둘러볼 때는 HTTP를 사용하고, 인스턴트 메시지를 주고받을 때는 XMPP를 사용하죠. 간단히 말해 FTP란 파일을 이동할 때 사용하는 프로토콜이라고 보시면 됩니다.

## section17

- **SQS Request-Response Systems**
  - 메시지별로 응답 대기열을 생성하지 마십시오. 그 대신 시작할 때 생산자별로 응답 대기열을 생성하고 상관 ID 메시지 속성을 사용하여 응답을 요청에 매핑합니다.

  - 생산자가 응답 대기열을 공유할 수 없도록 하십시오. 이로 인해 생산자는 다른 생산자를 위한 응답 메시지를 수신할 수 있습니다.

  - *SQS Temporary Queue Client* 요청-응답 메시징 패턴(가상 대기열) : 임시 대기열의 가장 일반적인 사용 사례는 요청-응답 메시징 패턴

- **Shard**
  - 샤드는 스트림에서 고유하게 식별되는 데이터 레코드 시퀀스입니다. 스트림은 하나 이상의 샤드로 구성되며 각 샤드는 고정된 용량 단위를 제공합니다. 각 샤드는 읽기에 대해 초당 최대 5개의 트랜잭션, 최대 총 데이터 읽기 속도 (초당 2MB), 초당 최대 1,000개의 레코드를 지원할 수 있습니다. 최대 총 데이터 쓰기 속도는 초당 1MB (파티션 키 포함) 입니다. 스트림의 데이터 용량은 스트림에 지정하는 샤드 수의 함수입니다. 스트림의 총 용량은 해당 샤드의 용량의 합계입니다. 데이터 속도가 증가하면 스트림에 할당된 샤드 수를 늘리거나 줄일 수 있습니다.


## section18
- **Docker**
  - Docker is a software development platform to deploy apps
  - Apps are package in containers that can be run on any OS
  - Docker containers are created from Docker image and these images are stored in Docke repositories

- **Hypervisor**
  - 하이퍼바이저는 가상 머신(Virtual Machine, VM)을 생성하고 구동하는 소프트웨어입니다. 가상 머신 모니터(Virtual Machine Monitor, VMM)라고도 불리는 하이퍼바이저는 하이퍼바이저 운영 체제와 가상 머신의 리소스를 분리해 VM의 생성과 관리를 지원합니다.
  - 하이퍼바이저의 장점
    - 가상 머신(VM)은 동일한 물리적 하드웨어에서 구동할 수 있지만 논리적으로는 서로 분리돼 있다. 즉, 한 VM에 오류가 발생하거나 작동이 멈추거나 악성코드 공격을 받아도 같은 시스템내 다른 VM 혹은 다른 시스템으로도 확장되지 않는다는 의미다. VM은 또한 이동성이 매우 강하다. 하드웨어와 독립적이기 때문에 로컬 또는 원격 가상화 서버 사이를 이동할 수 있다. 물리적 하드웨어에 묶여 있는 전통적인 응용 프로그램에 비해 훨씬 이전이 수월하다.
  - container vs. Hypervisor
    - 최근 들어 컨테이너 기술은 하이퍼바이저의 잠재적인 대체재로 인기가 높다. 가상 머신보다 더 많은 응용프로그램을 하나의 물리적 서버에 넣을 수 있기 때문이다.

    - VM은 시스템 자원을 많이 잡아먹는다. 각 VM은 운영 체제의 전체 복제본 뿐만 아니라 운영 체제가 실행해야 하는 모든 하드웨어의 가상 복제본을 구동한다. 이로 인해 소모되는 RAM과 CPU가 빠른 속도로 늘어난다. 반면, 컨테이너에 필요한 것은 운영 체제, 지원 프로그램과 라이브러리, 특정 프로그램을 실행할 시스템 자원이면 충분하다.

- **mount**
  - Mounting a file system attaches that file system to a directory (mount point) and makes it available to the system. 
  - 물리적인 장치를 특정위치 디렉터리에 연결시켜주는 것
  - **PnP** : Plug and Play (디바이스를 꼽기만 하면 알아서 설정하고 플레이되는..) : 리눅스의 경우 특히 서버 환경의 경우는 PnP 기능이 작동하지 않고 관리자가 직접 mount 작업을 수행해야함

- **POD**
  - 파드 는 (고래 떼(pod of whales)나 콩꼬투리(pea pod)와 마찬가지로) 하나 이상의(도커 컨테이너 같은) 컨테이너 그룹이다. 이 그룹은 스토리지/네트워크를 공유하고, 해당 컨테이너를 구동하는 방식에 대한 명세를 갖는다. 파드의 콘텐츠들은 항상 함께 배치되고 같이 스케줄되며, 공유 컨텍스트 내에서 구동된다. 파드는 애플리케이션에 특화된 "논리 호스트"를 모델로 하고 있다. 이것은 하나 또는 강하게 서로 결합되어 있는 여러 애플리케이션 컨테이너를 포함한다. 컨테이너 이전의 세상에서 같은 물리적 또는 가상의 머신에서 실행되는 것은 같은 논리적 호스트에서 실행되고 있는 것을 의미한다.
  - Pod
    - Pod 는 쿠버네티스에서 가장 기본적인 배포 단위로, 컨테이너를 포함하는 단위이다.
    - 쿠버네티스의 특징중의 하나는 컨테이너를 개별적으로 하나씩 배포하는 것이 아니라 Pod 라는 단위로 배포하는데, Pod는 하나 이상의 컨테이너를 포함한다.

## section19
- **production**
  - 실제 서비스를 위한 운영 환경
- **deployment**
  - 배포
  - 배포는 최종 사용자에게 결과물을 전달하는 과정이다. 내가 내 컴퓨터에서 동작하게 만든 코드를 다른 컴퓨터에서도 동작할 수 있도록 하는 것이다. 

## section20
- **Amamzon API Gateway**
  - Amazon API Gateway는 규모와 관계없이 REST 및 WebSocket API를 생성, 게시, 유지, 모니터링 및 보호하기 위한 AWS 서비스

- **REST API**
  - API Gateway의 REST API는 백엔드 HTTP 엔드포인트, Lambda 함수 또는 기타 AWS 서비스와 통합되어 있는 리소스 및 메서드의 모음
  - API Gateway 기능을 사용하여 생성에서 프로덕션 API 모니터링에 이르기까지 API 수명 주기의 모든 측면을 지원
  - API Gateway REST API는 클라이언트가 서비스에 요청을 보내고 서비스가 동기식으로 응답하는 요청/응답 모델을 사용
  - 이러한 종류의 모델은 동기식 통신을 사용하는 다양한 종류의 애플리케이션에 적합

- **Amazon Cognito**
  - Amazon Cognito는 웹 및 모바일 앱에 대한 인증, 권한 부여 및 사용자 관리를 제공
  - 사용자는 사용자 이름과 암호를 사용하여 직접 로그인하거나 Facebook, Amazon, Google 또는 Apple 같은 타사를 통해 로그인
  - Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily. Amazon Cognito scales to millions of users and supports sign-in with social identity providers, such as Apple, Facebook, Google, and Amazon, and enterprise identity providers via SAML 2.0 and OpenID Connect.

- **STS(Security Token Service)**
  - AWS provides AWS Security Token Service (AWS STS) as a web service that enables you to request temporary, limited-privilege credentials for AWS Identity and Access Management (IAM) users or for users you authenticate (federated users). 

- **Read Capacity Units and Write Capacity Units(RCU WCU)**
  - [읽기 용량 단위 및 쓰기 용량 단위](https://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html#HowItWorks.SwitchReadWriteCapacityMode)

- **DAX Caching layer**
  - Amazon DynamoDB Accelerator(DAX)는 Amazon Virtual Private Cloud(Amazon VPC) 환경 내에서 실행되도록 설계
  - Amazon VPC 서비스는 기존 데이터 센터와 매우 유사한 가상 네트워크를 정의
  - VPC를 사용하면 IP 주소 범위, 서브넷, 라우팅 테이블, 네트워크 게이트웨이 및 보안 설정을 통제
  - Amazon VPC 보안 그룹을 사용하여 가상 네트워크에서 DAX 클러스터를 시작하고 클러스터에 대한 액세스를 제어

- **DynamoDB Streams**
  - DynamoDB Streams enable DynamoDB to get a changelog and use that changelog to replicate data across replica tables in other AWS Regions.

- **CloudFront** - **S3** : Enhanced security with CloudFront Origin Access Identity (OAI)

- **s3 transfer acceleration**
  - Amazon S3 Transfer Acceleration can speed up content transfers to and from Amazon S3 by as much as 50-500% for long-distance transfer of larger objects.

- **S3 Security**
  - Pre-Signed URLs: URLs that are valid only for a limited time (ex: premium video service for logged in users)

- **CloudFront Signed URL / Signed Cookies**
  - Signed URL = access to individual files

- **AWS IoT Core**
  - AWS IoT Core는 인프라를 관리하지 않고도 수십억 개의 IoT 디바이스를 연결하고, 수조 개의 메시지를 AWS 서비스에 라우팅 할 수 있게 함
- **Kinesus Data Streams**
  - pipe big data in real time
- **Kinesus Data Firehose**
  - load data stream into AWS data store

- **Athena**
  - Serverless query service to perform analytics against S3 objects
  - analyze data in S3 using serverless SQL, use Athena
  - Athena is a serverless SQL service and results are stored in S3

- **Redshift**
  - Redshift is based on PostgreSQL

- *AWS Lambda Limits to Know - per region*
  - maximum execution : 15min

- Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds. Amazon CloudFront can be used in front of an Application Load Balancer. // CloudFront는 global 한 usage뿐만 아니라 traffic 분산처리에도 도움

## section21

- **OLTP VS OLAP**
  - OLTP is what most people thinks of databases. It stands for Online Transactional Processing and is designed to serve as a persistent state store for front-end applications. They excel at quickly looking up specific information as well as transactional procedures like INSERT, UPDATE, or DELETE.  
- **OLTP online Transaction processing**
  - INSERT와 같이 종종 사용되어지는, 혹은 규모가 작은 데이터를 불러올때 사용되는 SQL쿼리가 필요할때 유용 -> xm
  - ex) Order # 210에만 해당되는 이름, 주소, 시간 정보 INSERT
- **OLAP - online analytical processing**
  - 매우 큰 데이터를 불러올때 사용. 주로 덩치가 큰 SELECT 쿼리가 사용됨 -> 조인, select, 트랜잭션 프로세싱이 쓰이지 않음
  - ex) 특정 회사 부서의 Net Profit, Products

- **AWS ElastiCache for Redis**
  - Amazon ElastiCache for Redis is a blazing fast in-memory data store that provides sub-millisecond latency to power internet-scale real-time applications.
  - *Redis* : 데이터베이스, 캐시, 메시지 브로커 및 대기열로 사용하는 빠른 오픈 소스 인 메모리 데이터 스토어

- **ElasticCache**
  - Amazon ElastiCache는 유연한 실시간 사용 사례를 지원하는 완전관리형 인 메모리 캐싱 서비스입니다. 캐싱에 ElastiCache를 사용하면 애플리케이션 및 데이터베이스 성능을 가속화할 수 있으며, 세션 스토어, 게임 리더보드, 스트리밍 및 분석과 같이 내구성이 필요하지 않는 사용 사례에서는 기본 데이터 스토어로 사용할 수 있습니다. ElastiCache는 Redis 및 Memcached와 호환 가능합니다.

- **What is sharding in ElastiCache?**
  - A shard is a collection of one or more nodes in an ElastiCache cluster. It is created to support *replication of data* into various nodes in the ElastiCache cluster so that cache remains reachable in case of loss of few nodes.

- **What is Presto or PrestoDB?**
  - Presto (or PrestoDB) is an open source, distributed SQL query engine, designed from the ground up for fast analytic queries against data of any size.


- **Kinesis Data Streams**
  - Streaming service for ingest at scale

- **Kinesis Data Firehose**
  - Load streaming data into S3 / Redshift / ES / 3rd party / custom HTTP

## section22
- **EC2 Detailed Monitoring**
    - This is a paid offering and is disabled by default. When enabled, the EC2 instance's metrics are available in 1-minute periods.

- **CloudWatch Custom Metrics**
    - High Resolution: 1/5/10/30 second(s) – Higher cost
    - Standard: 1 minute (60 seconds)

- *The number of EC2 instances in an ASG can not go below the minimum capacity, even if the CloudWatch alarm would in theory trigger an EC2 instance termination.*

- Amazon CloudWatch is a monitoring service that allows you to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. It is used to monitor your applications' performance and metrics.
    - *configuration change , want to evaluate the impact of the performance --> CloudWatch*

- **CloudTrail Insights**
    - Enable CloudTrail Insights to detect unusual activity in your account

- You can use the **CloudTrail Console** to view the **last 90 days*** of recorded API activity. For events older than 90 days, use Athena to analyze CloudTrail logs stored in S3.
    - Analyze CloudTrail logs in S3 bucket using Amazon Athena

- **AWS Config Rules**
    - AWS Config Rules does not prevent actions from happening
    - Can make custom config rules (must be defined in AWS Lambda)
    - *Config Rules – Remediations*
        - Automate remediation of non-compliant resources using SSM Automation Documents
        - Which AWS Config feature can you use to automatically re-configure your Security Groups to their correct state?

## section23

- **Single sign-on (SSO)** is an authentication method that enables users to securely authenticate with multiple applications and websites by using just one set of credentials. 

- **SAML(Security Assertion Markup Language)**은 네트워크를 통해 여러 컴퓨터에서 보안 자격 증명을 공유할 수 있도록 하는 공개 표준이다. 한 대의 컴퓨터가 하나 이상의 다른 컴퓨터를 대신해 몇 가지 보안 기능을 수행할 수 있도록 하는 프레임워크를 설명한다.
  - 인증(Authentication) : 사용자가 자신이 주장하는 사람임을 확인
  - 허가(Authorization) : 사용자가 특정 시스템이나 콘텐츠에 접속할 수 있는 권한이 있는지 확인

  - 엄밀히 말하면 SAML은 모든 정보를 인코딩하는 데 사용되는 XML 변형 언어를 의미한다. 하지만 이 용어는 표준의 일부를 구성하는 다양한 프로토콜 메시지와 프로파일을 포함할 수 있다. 

  - SAML 2.0은 2005년에 도입됐으며, 현재 표준으로 남아있다. 이전 버전인 1.1은 이제 거의 사용하지 않는다. 
  
- SAML(Security Assertion Markup Language)은 사용자 ID, 인증 및 속성 정보를 표시하고 교환하기 위한 OASIS 개방형 표준입니다. SAML 어설션은 싱글 사인온 요청을 완료하는 일부로서 사용자 ID 및 속성 정보를 사용자의 ID 제공자로부터 신뢰 서비스 제공자로 전송하기 위해 사용되는 XML 형식화된 토큰입니다. SAML 어설션은 연합 비즈니스 파트너 간에 정보를 전송하는 벤더 중립적인 수단을 제공합니다. SAML을 사용하여 엔터프라이즈 서비스 제공자는 별도의 엔터프라이즈 ID 제공자에 접속하여 보안 컨텐츠에 액세스를 시도 중인 사용자를 인증할 수 있습니다. 

- **ADFS (Active Directory Federation Service)**
  - 사용자 계정 및 응용 프로그램이 완전히 다른 네트워크나 조직에 있는 경우에도 하나 이상의 보호된 인터넷 연결 응용 프로그램에 대한 완벽한 "단일 프롬프트" 액세스를 가진 브라우저 기반 클라이언트(네트워크 내부 또는 외부)를 제공하는 ID 액세스 솔루션 이다

  - 응용 프로그램이 한 네트워크에 있고 사용자 계정이 다른 네트워크에 있을 경우 일반적으로 사용자가 응용 프로그램에 액세스하려고 할 때 보조 자격 증명을 묻는 메시지가 표시 됩니다.

  - 이러한 보조 자격 증명은 응용 프로그램이 상주하는 영역의 사용자 ID를 나타냅니다. 일반적으로 응용 프로그램을 호스팅하는 웹 서버에서 가장 적절한 권한 부여 결정을 내리는데 이러한 자격증명이 필요하다.

  - 쉽게 말하자면 ADFS는 Office 365, 클라우드 기반 SaaS Application, 내부의 Network, 내부의 Application의 다양한 엑세스 제어 및 Single Sign On (SSO) 를 제공합니다.

 
- **What is ADFS and how it works?**
  - What is ADFS? Active Directory Federation Services is a feature and web service in the Windows Server Operating System that allows sharing of identity information outside a company's network. It authenticates users with their usernames and passwords.

- **AWS prod**
  - A product is an IT service that you want to make available for deployment on AWS. 

- **AWS PCI**
  - AWS PCI Compliance is an Amazon Web Service (AWS) that is Payment Card Industry (PCI) compliant. 

- **IAM 역할과 리소스 기반 정책의 차이**
  - [IAM 역할과 리소스 기반 정책의 차이](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)
  - ID 기반 정책과 달리 리소스 기반 정책은 해당 리소스에 액세스할 수 있는 사용자(보안 주체)를 지정
  - 리소스 기반 정책을 통해 액세스한 리소스로 인해 보안 주체는 여전히 신뢰할 수 있는 계정에서 작업을 할 수 있고, 역할 권한을 수신하기 위해 **자신의 권한을 포기할 필요가 없습니다.** 즉, 보안 주체는 신뢰하는 계정의 리소스에 액세스하는 동시에 신뢰할 수 있는 계정의 리소스에 계속 액세스할 수 있습니다. 다른 계정의 공유 리소스로 정보를 복사하거나 공유 리소스의 정보를 복사하는 등의 작업에서 이는 특히 유용합니다. 

- You have a mobile application and would like to give your users access to their own personal space in the S3 bucket. How do you achieve that?
  - Never make an S3 bucket public to your mobile application users. This would result in data leaks!
  - **Amazon Cognito can be used to federate mobile user accounts and provide them with their own IAM permissions, so they can be able to access their own personal space in the S3 bucket.**

- **AWS RAM**
  - AWS *Resource Access Manager* (AWS RAM) helps you securely share your AWS resources within your organization or organizational units (OUs) in AWS Organizations and with AWS Accounts. You can also share resources with IAM Roles and IAM Users.

## section24
- **SSM**: AWS Systems Manager

-  Define Web ACL (Web Access Control List):
  - Protects from common attack - SQL injection and **Cross-Site Scripting (XSS)**
  - 사이트 간 스크립팅(또는 크로스 사이트 스크립팅, 영문 명칭 cross-site scripting, 영문 약어 XSS)은 웹 애플리케이션에서 많이 나타나는 취약점의 하나로 웹사이트 관리자가 아닌 이가 웹 페이지에 악성 스크립트를 삽입할 수 있는 취약점이다.
  - What is cross site scripting (XSS) Cross site scripting (XSS) is a common attack vector that injects malicious code into a vulnerable web application

- **In-flight Encryption = HTTPS**, and HTTPS can not be enabled without an SSL certificate.

- You need to create KMS Keys in AWS KMS before you are able to use the encryption features for EBS, S3, RDS ...
  - False
  - You could also create your own keys for AWS to do the encryption, but it's not mandatory.
  - You can use the AWS Managed Service keys in KMS, therefore we don't need to create our own KMS keys.

- You have a secret value that you use for encryption purposes, and you want to store and track the values of this secret over time. Which AWS service should you use?
  - SSM Parameters Store can be used to store secrets and has built-in version tracking capability. Each time you edit the value of a parameter, SSM Parameter Store creates a new version of the parameter and retains the previous versions. You can view the details, including the values, of all versions in a parameter's history.


## section25
- **octect**
  - 컴퓨터에서의 옥텟은 8 비트의 배열
  - octet-stream이라는 것은 말 그대로 8비트로 된 일련의 데이타
  - IPv4 주소에서의 옥텟이라는 말의 의미는 32비트의 IP 주소를 8비트로 나누는 단위라고 할수 있다. IP 주소는 32비트로 이루어져 있고, 그것을 옥텟(Octet)단위로 끊어서 표현한다. 각 옥텟은 10진수로 0~255의 값을 가지게 된다. 그리고 나누어진 옥텟을 마침표(.)단위로 나누어서 표기하는 것이다.
  - IPv4 주소는 총 32비트로 이루어져 있는데 4구간으로 나누어서 사용된다. 그래서 8비트씩 4구간으로 나누어서 사용하게 되는데 8비트씩 나누어진 것을 옥텟이라고 한다.
  - ![IPv4](https://qph.fs.quoracdn.net/main-qimg-a4e28e6d0a7c25607b8fb34a2956267f)


- **Cloud**
  - servers that are accessed over the internet, along with the software and databases that run on those servers


## section26

- **RPO an RTO**
  - RPO(Recovery Point Object) : 데이터 손실을 허용할 수 있는 최대 기간
  - RTO(Recovery Time Objective) : 장애 후 데이터를 복구하고 처리를 재개하는 데까지 최대 허용시간
  - 예를 들어 1시에 백업을 한다고 가정하면 6시에 장애가 나면 RPO는 5시간입니다. 복구에 걸리는 시간이 3시간이어서 9시에 복구가 완료되었다고 한다면 RTO는 3시간입니다. RPO와 RTO를 줄이기 위해서는 비용이 수반되는데, 이를 위해서 업무중요도 및 영향도에 따라서 RPO와 RTO를 고려하여 재해복구 또는 무중단 인프라를 구축하도록 설계하는 것이 최근의 인프라 스트럭처 트렌드입니다.
  - Recovery point objective (RPO): The maximum acceptable amount of time since the last data recovery point.
  - Recovery time objective (RTO): The maximum acceptable delay between the interruption of service and restoration of service. This determines an acceptable length of time for service downtime. 
  
- **Downtime**
  - 다운타임(downtime 또는 outage duration)은 시스템을 이용할 수 없는 시간
  - 사용사능한 가동시간 uptime

- [point-in-time recovery (PITR)](https://aws.amazon.com/ko/blogs/storage/point-in-time-recovery-and-continuous-backup-for-amazon-rds-with-aws-backup/)

- Server Messaging protocol (SMB) protocol
- Network File System (NFS) protocol 

- AWS DataSync is an online data transfer service that simplifies, automates, and accelerates moving data between on-premises storage systems and AWS Storage services, as well as between AWS Storage services.

## section27
- **DLQ**
  - A dead-letter queue is an Amazon SQS queue that an Amazon SNS subscription can target for messages that can't be delivered to subscribers successfully. 

- single root I/O virtualization (SR-IOV)
- **Amazon FSx for Lustre**
  - Lustre is a type of parallel distributed file system, for large-scale computing
  - The name Lustre is derived from “Linux” and “cluster”

- Bastion Hosts
  - public EC2 instance to SSH into, that has SSH connectivity to EC2 instances in private subnets


## section28

- **CI**
  - CI/CD의 "CI"는 개발자를 위한 자동화 프로세스인 지속적인 통합(Continuous Integration)을 의미
  - CI를 성공적으로 구현할 경우 애플리케이션에 대한 새로운 코드 변경 사항이 정기적으로 빌드 및 테스트되어 공유 리포지토리에 통합되므로 여러 명의 개발자가 동시에 애플리케이션 개발과 관련된 코드 작업을 할 경우 서로 충돌할 수 있는 문제를 해결할 수 있습니다.

- **CD**
  - CI/CD의 "CD"는 지속적인 서비스 제공(Continuous Delivery) 및/또는 지속적인 배포(Continuous Deployment)를 의미하며 이 두 용어는 상호 교환적으로 사용됩니다. 두 가지 의미 모두 파이프라인의 추가 단계에 대한 자동화를 뜻하지만 때로는 얼마나 많은 자동화가 이루어지고 있는지를 설명하기 위해 별도로 사용되기도 합니다.

- 지속적인 제공이란 개발자들이 애플리케이션에 적용한 변경 사항이 버그 테스트를 거쳐 리포지토리(예: GitHub 또는 컨테이너 레지스트리)에 자동으로 업로드되는 것을 뜻하며, 운영팀은 이 리포지토리에서 애플리케이션을 실시간 프로덕션 환경으로 배포할 수 있습니다. 이는 개발팀과 비즈니스팀 간의 가시성과 커뮤니케이션 부족 문제를 해결해 줍니다. 지속적인 제공은 최소한의 노력으로 새로운 코드를 배포하는 것을 목표로 합니다.

- 지속적인 배포(또 다른 의미의 "CD": Continuous Deployment)란 개발자의 변경 사항을 리포지토리에서 고객이 사용 가능한 프로덕션 환경까지 자동으로 릴리스하는 것을 의미합니다. 이는 애플리케이션 제공 속도를 저해하는 수동 프로세스로 인한 운영팀의 프로세스 과부하 문제를 해결합니다. 지속적인 배포는 파이프라인의 다음 단계를 자동화함으로써 지속적인 제공이 가진 장점을 활용합니다.

 
- **CloudFormation**
  - AWS에 구축한 configuration을 템플릿화하여 재사용하기 쉽게 해주는 서비스
  - AWS CloudFormation은 Amazon Web Services 리소스를 모델링하고 설정하여 리소스 관리 시간을 줄이고 AWS에서 실행되는 애플리케이션에 더 많은 시간을 사용하도록 해 주는 서비스입니다. 필요한 모든 AWS 리소스(예: Amazon EC2 인스턴스 또는 Amazon RDS DB 인스턴스)를 설명하는 템플릿을 생성하면 AWS CloudFormation이 해당 리소스의 프로비저닝과 구성을 담당합니다. AWS 리소스를 개별적으로 생성하고 구성할 필요가 없으며 어떤 것이 무엇에 의존하는지 파악할 필요도 없습니다. AWS CloudFormation에서 모든 것을 처리합니다. 다음 시나리오는 AWS CloudFormation이 얼마나 유용한지를 보여줍니다

- **Where are Docker images stored?**
  - ECR

- **CloudFormation StackSets** allows you to create, update, or delete CloudFormation stacks across multiple AWS accounts and AWS regions with a single operation.

- **ECS = Elastic Container Service**
  - Launch Docker containers on AWS
  - Which AWS service allows you to manage a fleet of Docker containers in AWS Cloud and on-premises?
  - Amazon ECS is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications.

- **AWS Glue**
  - It is a Serverless data-preparation service for extract, transform, and load (ETL) operations.

- **AWS OpsWorks** is a configuration management service that provides managed instances of **Chef and Puppet**.

- AWS **AppSync** is a fully managed service that makes it easy to develop **GraphQL** APIs by handling the heavy lifting of securely connecting to data sources like DynamoDB, Lambda, and more



## Practice_Exam 
- **Blue/green deployment** is a technique for releasing applications by shifting traffic between two identical environments running different versions of the application: "Blue" is the currently running version and "green" the new version. This type of deployment allows you to test features in the green environment without impacting the currently running version of your application. When you’re satisfied that the green version is working properly, you can gradually reroute the traffic from the old blue environment to the new green environment. Blue/green deployments can mitigate common risks associated with deploying software, such as downtime and rollback capability.


- **AWS Trusted Advisor** : Analyze your AWS accounts and provides recommendation
  - Which AWS Service analyzes your AWS account and gives recommendations for cost optimization, performance, security, fault tolerance, and service limits?
  - AWS Trusted Advisor provides recommendations that help you follow AWS best practices. It evaluates your account by using checks. These checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas.
  - Trusted Advisor는 수십만 명의 AWS 고객에게 서비스를 제공하면서 익힌 모범 사례를 활용합니다. Trusted Advisor는 AWS 환경을 검사한 후 비용 절감, 시스템 가용성 및 성능 향상 또는 보안 격차를 해결할 기회가 있을 때 권장 사항을 제시합니다.

- **Amazon CloudFront**
	- Amazon CloudFront는 .html, .css, .js 및 이미지 파일과 같은 정적 및 동적 웹 콘텐츠를 사용자에게 더 빨리 배포하도록 지원하는 웹 서비스입니다. CloudFront는 엣지 로케이션이라고 하는 데이터 센터의 전 세계 네트워크를 통해 콘텐츠를 제공합니다.
  - CloudFront를 통해 서비스하는 콘텐츠를 사용자가 요청하면 지연 시간이 가장 낮은 엣지 로케이션으로 요청이 라우팅되므로 가능한 최고의 성능으로 콘텐츠가 제공됩니다.

- Lambda , log , analysis --> **CloudWatch Execution log**

- Load balancer 는 항상 public subnet에 두는 것으로 알고있어야.
- 특정기간내에 삭제 --> Lifecycle

- **s3 intelligent tiering**
  - 여기서 S3 Intelligent-Tiering은 객체 기준으로 액세스 요청의 빈도수에 따라 알아서 객체의 티어를 S3 Standard, S3 Standard-IA 분류해주는 기능이었다.
  - (30일 동안 액세스가 없으면 객체가 Stadard-IA로 이동 / 액세스가 발생되면 다시 Stadard로 이동)

- S3 – CloudFront(CDN) : CloudFront와 S3 사이의 데이터흐름은 공짜 
  - CloudFront : 엣지 서비스
  - 한국의 영상을 미국의 엣지서버로 CDN 엣지 캐시 호출해서 response타임을 줄일 수 있음
  - Response 타임 줄이고
  - 보안강화

- 우선 DB는 절대 Public subnet에 놓지 않습니다.

- ? VPC Routing ?
  - Redshift Enhanced VPC Routing: COPY / UNLOAD goes through VPC

- Instance store은 EBS랑 비슷한 temporary 용 저장장소 (Ec2 에 딱붙어있는 저장장치 EBS보다 10배빠름..Ec2꺼지면 instace store에있는 정보 날아감)

- **!!Disk RAID : 이거 기본적인 면접질문!!**

- 데이터 파이트라인으로 전달
  - Kinesis (real time / coorinate)
  - SQS


- 보안적으로 안전하게 설정하는 방법
  - Web서버의 ip를 DB security 그룹에 넣는 것은 좋지않습니다.
  - Web서버의 security group을 소스로 DB security 그룹에 넣어야

- Config는 aws 자원의 설정을 확인/백업/롤백

- 인증서 certification --> SNI
  - SNI solves the problem of loading multiple SSL certificates onto one web server (to serve multiple websites)

- AWS Organization service : RAM 
  - Resource Access MAnager

- proportionately이란 단어 -->  weighted routing

- Auto Scaling Groups - Scaling Cooldowns

- 서로다른 VPC간 접근하고싶다 --> VPC Peering
  - Cf ) Transit Gateway – transitive peering connections for VPC, VPN & DX

- Low inter-node latency
  - Cluster placement Groups

- Hibernating : 인스턴스를 끄게 되면 컴퓨팅비용은 안들고 elastic IP 와 디스크비용 ebs 비용만 추가됨

- AWS 내의 flow log  --> VPC Flow log

<!--
- [Basic Newtork Tips](https://6kkki.tistory.com/14)
- **IP주소**
  - IP (*Internet + Protocol*)
  - Internet은 이름처럼 inter + network 를 의미
  - 여러개의 소규모 네트워크들이 연결되어 거대한 네트워크를 이루는 것
  - 전산실에 있는 컴퓨터들을 ethernet 케이블 등을 이용해서 물리적으로 연결하면 소규모 네트워크가 됨
  - 이를 LAN (*Local Area Network*)이라고 함
  - LAN + LAN ==> Internet
  - 인터넷 상에서 컴퓨터 간의 제어나 연결 혹은 통신과 데이터 전송에 대한 규약
  - 어떤 한 컴퓨터를 찾아낼 수 있는 주소

- **Gateway**
  - LAN은 입구역할을 하는 컴퓨터를 통해 외부 네트워크와 연결 -> 그 컴퓨터가 Gateway
  - Gateway : 다른 네트워크로 들어가는 입구역할을하는 네트워크 point

- **DNS**
  - 컴퓨터 네트워크에서 장치들이 서로를 인식하기 위해서, 그리고 IP를 다 하나하나 외울 수 없기 때문에 DNS가 등장
  - DNS : 특정 컴퓨터의 주소를 찾기 위해, 사람이 이해하기 쉬운 도메인이름을 숫자로 된 식별번호로 변환

- **subnet**
  - subnetwork를 줄인말
  - 어떤 기관에 소속된 네트워크이지만 따로 분리되어 있는 한 부분으로 인식될 수 있는 네트워크를 의미

- 서브넷을 보면 255와 0으로 구성이 되어 있다. 네트워크 부분은 255로, 호스트 부분은 0으로 지정해서 IP주소의 어디까지가 네트워크 주소이고 어디부터가 호스트 주소인지 알 수 있다.

  - 예를 들어, subnet이 255.255.0.0 이고 IP 주소가 1.2.3.4 라면, 1.2 까지가 네트워크 주소이고 3.4는 호스트 주소가 된다. 다시 예를 들어 subnet이 255.255.255.0 이고 IP 주소가 1.2.3.4라면 1.2.3까지가 네트워크 주소이고 마지막 4가 호스트 주소가 되는 것이다. 

  - 그렇다면 네트워크 부분과 호스트 부분은 정확히 어떠한 것을 정의하는 것일까? 
    - 네트워크 부분은 통신을 위해서 데이터를 전송하였을 때 라우터를 거치지 않고 전송이 가능한 영역이라는 뜻이다. 호스트 부분은 각각의 PC를 말하는 것이다.
  - 예시를 보면 조금 이해가 빠를 것이다. 호스트 3개가 있다고 치자. 
  - 호스트 a의 IP는 210.170.1.1, 호스트 b의 IP는 210.170.1.2, 호스트 c의 IP는 210.170.2.1이라고 하자.

  - 만일 이 호스트들의 써브넷마스크가 255.255.255.0이라고 하면 네트워크 주소 부분이 세번째 부분까지 된다. 따라서 210.170.1.까지 같은 a와 b는 같은 네트워크로 직통연결이 가능하다.

  - 만약 써브넷마스크가 255.255.0.0이라면 a,b,c 모두 같은 네트워크가 되어 직통연결이 가능한 것이다.
-->

- Elastic Load Balancing 
  - Application Load Balancers, Network Load Balancers, Gateway Load Balancers 및 Classic Load Balancer 각자 필요에 따라 가장 적합한 로드 밸런서 유형을 선택할 수 있습니다.


- **Network Load Balancer – Target Groups**
  - *EC2 instances*
  - IP Addresses : *must be private IPs*
  - If you specify targets using an instance ID, traffic is routed to instances using the primary private IP address specified in the primary network interface for the instance. 

- ( 7 ) 
- **NAT Gateway**는 Newtwork Address Transition 네트워크 주소변환서비스
  - NAT 게이트웨이: 프라이빗 서브넷에 있는 리소스가 인터넷에 액세스할 수 있게 해주는 고가용성 관리형 네트워크 주소 변환 (NAT) 서비스입니다.
  -  Subnet 을 Public 과 Private 으로 구분하여, Public subnet은 Internet Gateway 를 이용하여 외부와 통신이 가능하도록 설정하였다. 하지만, Private Subnet 의 경우는 외부와의 통신이 단절된 환경이다.
    - Private Subnet에 위치한 instance가 다른 AWS 서비스에 연결해야 하는 경우. 
    - 인터넷에서 Private instance 에 접근 불가 조건은 유지하면서 반대로 instance 에서 외부 인터넷으로 연결이 필요한 경우. 
  -  위와 같은 이유로 Private Subnet에 배포된 instance 라도 외부와의 통신이 필요한 경우가 있다. 이런 경우 가장 간단히 해결 할 수 있는 방법은 NAT 서버를 구축하는 것이다.
  - *NAT Gateway : managed by AWS, provides scalable Internet access to private EC2 instances, IPv4 only*

- **NAT Instance**
  - *NAT Instances : gives Internet access to EC2 instances in private subnets. Old, must be setup in a public subnet, disable Source / Destination check flag*
  - *You must manage Security Groups*
  - *Use as Bastion Host*
  - *Support port fowarding*

- **Bastion host**
  - [Bastion host concept](https://bluese05.tistory.com/48)
  - Bastion Host : public EC2 instance to SSH into, that has SSH connectivity to EC2 instances in private subnets
  - Private Subnet에 배포된 instance의 경우 외부에서 접근이 차단되어 있기 때문에 SSH 로 접근할 수 있는 방법이 없다. 하지만 운영자는 서버를 관리 하기 위해 SSH 접속이 필요하다. 이러한 경우 Bastion host 라는 방식으로 외부 접근이 가능하도록 구성한다.  

  - Bastion host는 Private 네트워크 환경에 접근하기 위한 일종의 Proxy 역할을 하는 서버라고 보면 된다.  Private subnet에 배포된 모든 instance 들은 bastion을 통해 SSH 접속을 허용하도록 한다. 접근 허용을 한 곳으로 한정 지음으로 좀 더 보안성을 높이고자 하는 목적이 있으며 bastion host의 logging 만 관리하면 private subnet에 접속하는 모든 기록을 관리할 수 있다. 
  -  단, bastion host 가 공격 당하면 내부 네트워크가 모두 위험해 질 수 있으므로 bastion host에 대한 접근을 최대한 철저히 관리하는게 좋다. 

  - Bastion host는 Public Subnet에 위치하도록 EC2 instance를 생성한다. 외부 사용자는 Bastion host 를 통해 접속한다. 
  - 외부 사용자의 특정 IP만 허용하여 Bastion host에 접속 가능하도록 ACL 과 Security Group을 설정한다. 
  - Bastion host 를 통해 Private Subnet에 상주한 instance 로 접속 한다. 

- **Direct Connect(DX)**
  - Provides a deciated private connection from a remote network to your VPC
  - Dedicated connection must be setup between your DC and AWS Direct Connect locations

- (8)
- **Site-to-Site VPN Connection**
  - Create a Virtual Private Gateway on the AWS side of the VPN and a Customer Gateway on the on-premises side of the VPN
  - enable Route Propagation for the VGW

- (9)
- EC2 Instance placement strategy (Cluster, Spread, Partition)
- **Cluster placement group**
  - clusters instances into a low-latency group in a single Availability Zone

- (11)
- **Cloud Hub**
  - *One VPC connect with multiple On Premise Network*
  - Use VPN to establish connection
- **Transit Gateway**
  - *Connect multiple VPC with multiple On Premise Network*
  - Use VPN and Direct Connect to establish connection
  - Supports IP Multi-cast
- **VPC Peering**
  - A VPC peering connection is a networking connection between *two VPCs* that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses.

- (12)
- **migrate from SQS Standard queues to FIFO queues**, the following steps should be the migration checklist
  - *Delete* the existing standard queue and recreate it as a FIFO queue
  - Make sure that the name of the FIFO queue ends with the *.fifo* suffix
  - Make sure that the throughput for the target FIFO queue does not exceed *3,000* messages per second
    - (Limited throughput: 300 msg/s without batching, 3000 msg/s with)

- (13)
- **AWS X-Ray**
  - AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. 
  - *accross account debugging*
- **CloudTrail**
  - : With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. You can use AWS CloudTrail to answer questions such as - “Who made an API call to modify this resource?”. CloudTrail provides event history of your AWS account activity thereby enabling governance, compliance, operational auditing, and risk auditing *of your AWS account*. You cannot use CloudTrail to debug and trace data across accounts.
  - *debugging of your account*


- (14)
- **Amazon VPC console wizard configurations**
- [vpc console wizard](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_wizard.html)
  - VPC with a single public subnet
  - VPC with public and private subnets (NAT)
  - VPC with public and private subnets and AWS Site-to-Site VPN access
  - VPC with a private subnet only and AWS Site-to-Site VPN access
  - *VPC with a public subnet only and AWS Site-to-Site VPN access (X)*

- (15)
- data sources supported by **GuardDuty**
  - VPC Flow Logs, DNS logs, CloudTrail events 
  - VPC Flow Logs, DNS logs, CloudTrail events - Amazon GuardDuty is a threat detection service that continuously monitors for malicious activity and unauthorized behavior to protect your AWS accounts, workloads, and data stored in Amazon S3. 


- (16)
- **EBS encryption**
  - [EBS encryption](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html)
    - Data at rest inside the volume
    - All data moving between the volume and the instance
    - All snapshots created from the volume
    - All volumes created from those snapshots
  - Amazon Elastic Block Store (Amazon EBS) provides block-level storage volumes for use with EC2 instances. When you create an encrypted EBS volume and attach it to a supported instance type, data stored at rest on the volume, data moving between the volume and the instance, snapshots created from the volume and volumes created from those snapshots are all encrypted.

- (19)
- **Protection for objects stored in S3**
  - *Enable MFA delete on the bucket*
  - *Enable versioning on the bucket*

- (20)
  - **A permissions boundary** can be used to control the maximum permissions employees can grant to the IAM principals (that is, users and roles) that they create and manage.

- (21)
- **ASG Lifecycle Hooks** : ASG custom action
  - Auto Scaling group lifecycle hooks enable you to perform custom actions as the Auto Scaling group launches or terminates instances. Lifecycle hooks enable you to perform custom actions by pausing instances as an Auto Scaling group launches or terminates them. 

- (22)
  - **ElastiCache for Redis**
    - Amazon ElastiCache for Redis is a blazing fast in-memory data store that provides sub-millisecond latency to power internet-scale real-time applications. Amazon ElastiCache for Redis is a great choice for *real-time transactional and analytical processing* use cases 

  - **ElastiCache for Memchached**
    - Amazon ElastiCache for Memcached is a Memcached-compatible in-memory key-value store service that can be used as a cache or a data store. Amazon ElastiCache for Memcached is a great choice for implementing an in-memory cache to decrease access latency, increase throughput, and ease the load off your relational or NoSQL database. Session stores are easy to create with Amazon ElastiCache for Memcached. 

- (23)
- In the exam: **Chef & Puppet** needed => AWS Opsworks
- Chef & Puppet help you perform server configuration automatically, or repetitive actions

- (24)
- DMS Sources and Targets
  - SOURCES:
  -  On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL,MongoDB, SAP, DB2
    - Azure: Azure SQL Database
    - Amazon RDS: all including Aurora
    - Amazon S3

  - TARGETS:
  - On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, SAP
    - Amazon RDS
    - Amazon Redshift
    - Amazon DynamoDB
    - Amazon S3
    - ElasticSearch Service
    - Kinesis Data Streams
    - DocumentDB

- (25)
- **AWS Lambda**
  - Virtual functions – no servers to manage!
  - Integrated with the whole AWS suite of services
  - By default, Lambda functions always operate from an AWS-owned VPC and hence have access to any public internet address or public AWS APIs. Once a Lambda function is VPC-enabled, it will need a route through a NAT gateway in a public subnet to access public resources 
  - Since Lambda functions can scale extremely quickly, its a good idea to deploy a CloudWatch Alarm that notifies your team when function metrics such as ConcurrentExecutions or Invocations exceeds the expected threshold 
  - If you intend to reuse code in more than one Lambda function, you should consider creating a Lambda Layer for the reusable code 

- **ECS**
  - You must provision & maintain the infrastructure (the EC2 instances)
- **Fargate**
  - You do not provision the infrastructure (no EC2 instances to manage)

- (26)
- ElastiCache – Cache Security
  - **Redis auth**

- (27)
- **AWS Global Accelerator** 
  - Improves performance for a wide range of applications over TCP or UDP
  - Proxying packets at the edge to applications running in one or more AWS Regions.
  - Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP
  - Good for HTTP use cases that require static IP addresses
  - Good for HTTP use cases that required deterministic, fast regional failover
- **Amazon CloudFront**
  - Improves performance for both cacheable content (such as images and videos)
  - Dynamic content (such as API acceleration and dynamic site delivery)
  - Content is served at the edge
  - CloudFront is better for improving application resiliency to handle spikes in traffic

- (28)
- **Neptune**
  - Fully managed graph database
  - High relationship data

- (29)
- **Aurora Replica**
  - increase availability
  - scale the read operations (handle many read request)

- (30)
- S3 is a proprietary storage technology (unlike EFS / NFS)
  - You can use Amazon S3 to host a static website. 
- *CloudFront* : Great for static content that must be available everywhere
- *S3* : Great for dynamic content that needs to be available at low-latency in few regions

- (31)
- **RDS Read Replicas**
  - For RDS Read Replicas within the same region, you don’t pay that fee
  - In AWS there’s a network cost when data goes from one AZ to another
  
- (32)
- **Spread placement group of EC2 instances**
  - A spread placement group can span multiple Availability Zones in the same Region. You can have a maximum of **seven** running instances per Availability Zone per group.


- (33)
- **User Data**
  - By default, scripts entered as user data are executed with root user privileges
  - By default, user data runs only during the boot cycle when you first launch an instance

- (34)
- **Amazon S3 - Consistency Model**
  - subsequent read request immediately receives the latest version of the object

- (35)
- **AWS Shield Standard** is automatically enabled for all AWS customers at no additional cost. AWS Shield Advanced is an optional paid service.


- (37)
- **Snowball Edge (for data transfers)**
  - Physical data transport solution: move *TBs or PBs of data* in or out of AWS
  - Transfer the on-premises data into multiple Snowball Edge Storage Optimized devices. Copy the Snowball Edge data into Amazon S3 and create a lifecycle policy to transition the data into AWS Glacier
  -  The data stored on the Snowball Edge device can be copied into the S3 bucket and later transitioned into AWS Glacier via a lifecycle policy. **You can't directly copy data from Snowball Edge devices into AWS Glacier.**


- (38)
- CloudWatch Alarm Targets
  - Stop, Terminate, Reboot, or Recover an EC2 Instance
  - Trigger Auto Scaling Action
  - Send notification to SNS
  - *Using CloudWatch event or CloudWatch alarm to trigger a lambda function, directly or indirectly, is wasteful of resources. You should just use the EC2 Reboot CloudWatch Alarm Action to reboot the instance. So all the options that trigger the lambda function are incorrect.*

- (39)
- **Amazon FSx for Lustre**
  - Lustre is a type of parallel distributed file system, for large-scale computing
  - FSx for Lustre provides the ability to both process the 'hot data' in a parallel and distributed fashion as well as easily store the 'cold data' on Amazon S3. 
  - Seamless integration with S3

- AWS Glue - AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics. 
- Amazon EMR - Amazon EMR is the industry-leading cloud big data platform for processing vast amounts of data 

- (40)
  - **VPC sharing** (part of Resource Access Manager) allows multiple AWS accounts to create their application resources such as EC2 instances, RDS databases, Redshift clusters, and Lambda functions, into shared and centrally-managed Amazon Virtual Private Clouds (VPCs).

- (41)
  - **Bucket policies** in Amazon S3 can be used to add or deny permissions across some or all of the objects within a single bucket.
  - **IAM policies** are attached to the users, enabling centralized control of permissions for users under your AWS Account to access buckets or objects. With IAM policies, you can *only grant users within your own AWS account permission* to access your Amazon S3 resources.

- (42)
  - You should use enhanced fan-out if you have multiple consumers retrieving data from a stream in parallel. 

- (43)
  - Use CloudTrail to analyze API calls - AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services.

  - In general, to analyze any API calls made within an AWS account, CloudTrail is used.
  - **debugging --> CloudTrail**


- (46)
- Instantiating EC2 Instances quickly
  - Use a Golden AMI: Install your applications, OS dependencies etc.. beforehand and launch your EC2 instance from the Golden AMI
  - Bootstrap using User Data: For dynamic configuration, use User Data scripts
  - Hybrid: mix Golden AMI and User Data (Elastic Beanstalk)

- (47)
- 

- (48)
- 







