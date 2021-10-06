---
title: "AWS - AWS Cloud Technical Essentials"
categories:
  - AWS
tags:
  - AWS
---

> **Work hard, have fun, and make history.**  
> [AWS Cloud Technical Essentials](https://www.edx.org/course/aws-cloud-technical-essentials)


# AWS Cloud Technical Essentials
> [Week1](#Week1)  
> [Week2](#Week2)  
> [Week3](#Week3)  
> [Week4](#Week4)  

## Week1

### Getting Start with AWS Cloud
- **What is AWS?**
    - As internet usage became more widespread, the demand for compute, storage, and networking equipment increased. For some companies and organizations, the cost of maintaining a large physical presence was unsustainable. To solve this problem, cloud computing was created.

    - Cloud computing is the on-demand delivery of IT resources over the internet with pay-as-you-go pricing. You no longer have to manage and maintain your own hardware in your own data centers. Companies like AWS own and maintain these data centers and provide virtualized data center technologies and services to users over the internet.
- **The Six Benefits of Cloud Computing**
    - `Pay as you go` : pay only for how much you use.
    - `Benefit from massive economies of scale` :  AWS can achieve higher economies of scale, which translates into lower pay as-you-go prices.
    - `Stop guessing capacity` : You can access as much or as little capacity as you need, and scale up and down as required with only a few minutes notice.
    - `Increase speed and agility` : IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes. 
    - `Stop spending money running and maintaining data centers`
    - `Go global in minutes`
- **AWS Global Infrastructure**
    - *This cluster of data centers is called an Availability Zone or AZ.*
    - *An AZ consists of one or more data centers with redundant power, networking, and connectivity.*

    - *A cluster of AZs is simply called a region.*
    - *And how do you choose a region?*
        - *By looking at compliance,latency, pricing, and service availability.*
    - *Maintain Resiliency by multiple AZs*

- **Ways to interact with the AWS API**
    - The AWS Management Console
    - The AWS Command Line Interface (CLI)
    - The AWS Software Development Kits (SDK)
        - API calls to AWS can also be performed by executing code with programming languages. You can do this by using AWS Software Development Kits (SDKs). SDKs are open-source and maintained by AWS for the most popular programming languages, such as C++, Go, Java, JavaScript, .NET, Node.js, PHP, Python, and Ruby.

- [Exercise 1: Create an AWS Account](https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/lab-1-account.html)

### Security in the AWS Cloud
- **hypervisor**
    - 하이퍼바이저는 가상 머신(Virtual Machine, VM)을 생성하고 구동하는 소프트웨어입니다. 가상 머신 모니터(Virtual Machine Monitor, VMM)라고도 불리는 하이퍼바이저는 하이퍼바이저 운영 체제와 가상 머신의 리소스를 분리해 VM의 생성과 관리를 지원합니다.
    - 서로 다른 여러 개의 운영 체제를 나란히 구동할 수 있으며, 하이퍼바이저를 사용해 동일한 가상화 하드웨어 리소스를 공유합니다. 바로 이러한 부분이 가상화의 핵심적인 이점입니다

- **Security and the AWS Shared Responsibility Model**
    - When you begin working with the AWS Cloud, managing security and compliance is a shared responsibility between AWS and you.

- **Protect the AWS Root User**
    - The email address you sign up with becomes the *root user* of the AWS account.

- **MFA**
    - Single-factor authentication is not recommended
    - you enable multi-factor authentication(MFA) for the root user.
    - MFA introduces an additional unique piece of information that you need

### AWS Identity and Access Management
- **IAM**
    - In fact, all API calls in AWS must be both signed and authenticated in order to be allowed - no matter if the resources live in the same account or not.
    - AWS IAM manages 
        - the login credentials and permissions to the AWS account itself
        - and it also can manage credentials used to sign API calls made to AWS services.
//
https://learning.edx.org/course/course-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@sequential+block@3e83ddce20fc46db8cc094f9ad0b2874/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@vertical+block@df850bc4e6d84910bc65e588b4dafc02


### Week 1 Assessment and Discussion


## Week2