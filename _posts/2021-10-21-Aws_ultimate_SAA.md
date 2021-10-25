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
    



