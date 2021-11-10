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

  