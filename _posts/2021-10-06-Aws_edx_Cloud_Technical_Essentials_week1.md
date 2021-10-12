---
title: "AWS - AWS Cloud Technical Essentials_week1"
categories:
  - AWS
tags:
  - AWS
---

> **Work hard, have fun, and make history.**  
> [AWS Cloud Technical Essentials](https://www.edx.org/course/aws-cloud-technical-essentials)

# AWS Cloud Technical Essentials - Week1

## Getting Start with AWS Cloud
- **What is AWS?**
    - As internet usage became more widespread, the demand for compute, storage, and networking equipment increased. For some companies and organizations, the cost of maintaining a large physical presence was unsustainable. To solve this problem, cloud computing was created.

    - Cloud computing is the on-demand delivery of IT resources over the internet with pay-as-you-go pricing. You no longer have to manage and maintain your own hardware in your own data centers. Companies like AWS own and maintain these data centers and provide virtualized data center technologies and services to users over the internet.
- **The Six Benefits of Cloud Computing**
    - Pay as you go  
        - pay only for how much you use.
    - Benefit from massive economies of scale
        - AWS can achieve higher economies of scale, which translates into lower pay as-you-go prices.
    - Stop guessing capacity 
        - You can access as much or as little capacity as you need, and scale up and down as required with only a few minutes notice.
    - Increase speed and agility 
        - IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes. 
    - Stop spending money running and maintaining data centers
    - Go global in minutes
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

## Security in the AWS Cloud
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

## AWS Identity and Access Management
- **IAM (AWS 전체의 권한 통제 시스템)**
    - In fact, all API calls in AWS must be both signed and authenticated in order to be allowed - no matter if the resources live in the same account or not.
    - AWS IAM manages 
        - the login credentials and permissions to the AWS account itself
        - and it also can manage credentials used to sign API calls made to AWS services.
    - 일반적으로 접근 제어에 대한 이야기를 할 때, 인증과 인가로 나누어서 설명
        - 인증 autentification : 클라이언트가 자신이 주장하는 사용자와 같은 사용자인지를 확인하는 과정
        - 인가 authorization : 클라이언트가 하고자 하는 작업이 해당 클라이언트에게 허가된 작업인지를 확인하는 권한부여와 관련이 있는 과정   
    - I (Identity) : Who you are
        - AWS로 요청할 수 있는 보안주체를 AWS어카운트내에 만들어줌
        - root User는 AWS계정의 이메일 계정과 동일한 루트유저
        - root User는 너무많은 권한을 가지고 있고 이 권한은 제어할 수 없는 슈퍼유저임
        - 그래서 AWS에서 직접 만들 수 있는 보안 주체들이 있음 (User / Role)
            - IAM User : 고객이 User Name / Password를 입력하고 콘솔에 로그인을 할 때 사용하는 보안주체 (장기 credential으로 자격증명 - Access Key + Secret Key)
            - IAM Role : 정의된 권한 범위 내 AWS API를 사용할 수 있는 임시자격증명(Access Key + Secret Key + *Token*)

    - AM (Access Management) : What you can DO (AWS 에서의 인가)
        - 누가 어떤 리소스들에 대해 어떤일을 할 수 있는 권한을 가지는지를 정의하는 도구로 동작을 하게됨

    - IAM은 AWS계정안에 IAM 그룹과 사용자를 생성하여 접근 제어 및 권한 관리를 세분화 할 수 있습니다. 어떤 IAM 사용자는 EC2만 관리할 수 있고, 어떤 IAM사용자는 S3의 내용을 읽을 수만 있도록 구성할 수 있습니다. 따라서 전체 권한이 아닌 필요한 권한만 주기때문에 보안성이 높아집니다. IAM 그룹은 동일한 권한을 여러 IAM 사용자에게 적용시킬 때 편리합니다.

    - IAM 그룹과 사용자에게 권한을 설정하는 것과는 달리 EC2 인스턴스 전용으로 권한을 설정할 수 있습니다. 이것을 IAM Role이라고 합니다. IAM Role은 EC2인스턴스 뿐만아니라 다른 AWS계정, 페이스북, 구글계정 전용으로 권한을 설정할 수 있습니다.

- **IAM Policy**
    - Example

    ```json
    {
    "Version": "2012-10-17",
        "Statement": [{
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
        }]
    }

    {
    "Version": "2012-10-17",
        "Statement": [{
            "Effect": "Allow",
            "Action": [
                "iam: ChangePassword",
                "iam: GetUser"
                ]
            "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
        }]
    }
    ```

        - Effect : default Value is Deny
        - Action : Describes the specific actions that will be allowed or denied
            - ex ) where we are allowing the action of "S3:*". So that is all S3 actions against all S3 resources.
        - Resource : Specifies the object or objects that the statement covers

- [Exercise: Following IAM Best Practices](https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/lab-2-iam.html)

## Week 1 Assessment and Discussion (5/10)
> [Answer can be checked with comments of the markdown file](https://learning.edx.org/course/course-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@sequential+block@7e1bb4fe1be1474fb4f1450c75ee8cab/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@vertical+block@1866f60f81824bc59cbee6fdf6acecf4)  


### Question 1 (X)   
- What are the four main factors you should take into consideration when choosing a Region?  
    - Latency, price, service availability, and compliance
    - Latency, high availability, taxes, and compliance
    - Latency, taxes, speed, and compliance
    - Latency, security, high availability, and resiliency

<!--[Latency, price, service availability, and compliance]You should consider four main aspects when deciding which AWS Region to host your applications and workloads: latency, price, service availability, and compliance. Focusing on these factors will enable you to make the right decision when choosing an AWS Region. You can find this content in the AWS Global Infrastructure video.-->

> Do AWS costs vary by region?  
 **Pricing for AWS services varies by region.** In regions where the cost of land, fiber, electricity and taxes is less – we pass those savings on to our customers.  

### Question 2
1 point possible
- True or false: Every action you take in AWS is an API call.
    - True
    - False

<!--[TRUE] In AWS, every action you make is an API call that is authenticated and authorized. You can make API calls to services and resources through the AWS Management Console, the AWS Command Line Interface (CLI), or the AWS Software Development Kits (SDKs). This content is covered in Interacting with AWS.-->

### Question 3

- Which of the following best describes the relationship between Regions, Availability Zones and data centers?
    - Availability Zones are clusters of Regions. Regions are clusters of data centers.
    - Data centers are cluster of Availability Zones. Regions are clusters of Availability Zones.
    - Regions are clusters of Availability Zones. Availability Zones are clusters of data centers.
    - Data centers are clusters of Regions. Regions are clusters of Availability Zones.

<!--[Regions are clusters of Availability Zones. Availability Zones are clusters of data centers.] The AWS Global Infrastructure is nested for high availability and redundancy. AWS Regions are clusters of Availability Zones that are connected through highly availably and redundant high-speed links and Availability Zones are clusters of data centers that are also connected through highly available and redundant high-speed links. This content is covered in the AWS Global Infrastructure video.-->

### Question 4 (X) 
- Which of the following is a benefit of cloud computing?
    - Run and maintain your own data centers.
    - Increase time-to-market.
    - Overprovision for scale.
    - Go global in minutes.
<!--incorrect
Answer
Incorrect:There are six benefits of cloud computing. The correct answer for this question is “go global in minutes.” Going global in minutes means you can easily deploy your applications in multiple Regions around the world with just a few clicks. Check out the reading “What is AWS?”-->

### Question 5
- True or false: In the cloud, instead of physically managing hardware, you use services.
    - True
    - False


### Question 6 (X) 
- Which of the following is a best practice when securing the AWS root user?
    - A) Enable MFA for the root user
    - B) Using the root user for routine administrative tasks
    - C) Disabling or deleting the access keys associated with the root user
    - A and B
    - A and C
<!--incorrect
Answer
Incorrect:You use an access key (an access key ID and secret access key) to make programmatic requests to AWS. However, do not use your AWS account root user access key. The access key for your AWS account root user gives full access to all your resources for all AWS services, including your billing information. You cannot reduce the permissions associated with your AWS account root user access key.Therefore, protect your root user access key like you would your credit card numbers or any other sensitive secret. You should disable to delete any access keys associated with the root user, and you should also enable MFA for the root user. This information can be found in the videoProtect the AWS Root User and Reading 1.6.-->


### Question 7 (X)
- Users in your company are authenticated in your corporate network and want to be able to use AWS without having to sign in again. Which AWS authentication option should you use?
    - AWS Root User
    - IAM User
    - IAM Role
    - IAM Group
<!--incorrect
Answer
Incorrect:Instead of creating an IAM User for each employee that needs access to the AWS account, you should use IAM Roles to federate users. Read more here: https://aws.amazon.com/identity/federation/This information can be found in the video Role Based Access in AWS or Reading 1.8.-->


### Question 8
- Which of the following can be found in an IAM policy?
    - A) Effect
    - B) Action
    - C) Object
    - A and B
    - B and C

<!--A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. AWS evaluates these policies when an IAM principal (user or role) makes a request. Permissions in the policies determine whether the request is allowed or denied. Most policies are stored in AWS as JSON documents that are attached to an IAM identity (user, group of users, or role). The information in a policy statement is contained within a series of elements: • Version – Specify the version of the policy language that you want to use. As a best practice, use the latest 2012-10-17 version. • Statement – Use this main policy element as a container for the following elements. You can include more than one statement in a policy. • Sid (Optional) – Include an optional statement ID to differentiate between your statements. • Effect – Use Allow or Deny to indicate whether the policy allows or denies access. • Principal (Required in only some circumstances) – If you create a resource-based policy, you must indicate the account, user, role, or federated user to which you would like to allow or deny access. If you are creating an IAM permissions policy to attach to a user or role, you cannot include this element. The principal is implied as that user or role. • Action – Include a list of actions that the policy allows or denies. • Resource (Required in only some circumstances) – If you create an IAM permissions policy, you must specify a list of resources to which the actions apply. If you create a resource-based policy, this element is optional. If you do not include this element, then the resource to which the action applies is the resource to which the policy is attached. • Condition (Optional) – Specify the circumstances under which the policy grants permission. This information can be found in the video Introduction to Amazon Identity and Access Management or Reading 1.7-->

### Question 9
- True or false: IAM policies can restrict the actions of the AWS root user.
    - True
    - False
<!--The AWS account root user gives full access to all your resources for all AWS services, including your billing information. You cannot reduce the permissions associated with your AWS account root user access key. This information can be found in the videoProtect the AWS Root User and Reading 1.6-->


### Question 10 (X) 
- True or false: Using a username and password, as well as a one-time passcode, to log in to an account is an example of multi-factor authentication.
    - True
    - False
<!--incorrect
Answer
Incorrect:Multi-factor Authentication is an authentication method that requires the user to provide two or more verification factors to gain access to an AWS account. This information can be found in the videoProtect the AWS Root User and Reading 1.6.-->
