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


