---
title: "AWS - Introduction to AWS Identity and Access Management_week1"
categories:
  - AWS
tags:
  - AWS
---

> **Work hard, have fun, and make history.**  
> [Introduction to AWS Identity and Access Management](https://learning.edx.org/course/course-v1:AWS+AWS-OTP-AWSD13+3T2020/home)  



## Authentication and Authorization

- **Authentication**
    - A principal must be authenticated (signed in to AWS) using their credentials to send a request to AWS. 
- **Authorization**
    - You must also be authorized (allowed) to complete your request.
    - By default, all requests are denied. (In general, requests made using the AWS account root user credentials for resources in the account are always allowed.)

## What is AWS IAM

- **IAM User**
    - an AWS IAM user is an entity created to represent the person or application that interacts with AWS.
- **IAM Group**
    - a group is a collection of IAM users.
    - Groups enable you to specify permissions from multiple users at once, which would make it much easier to manage the permissions of those users.
    - *What you don't see is nested groups or groups contained within groups.*


## IAM Policy
> These are policies that are attached to IAM identities that grant permissions to that identity. A policy is a *JSON-formatted document* that is used to outline what is and is not allowed for the identity.

## Identity providers
- **IdP** 
    - If you already manage user identities outside of AWS, you can use IAM identity providers instead of creating IAM users in your AWS account. 
    - With an identity provider (IdP), you can manage your user identities outside of AWS and give these external user identities permissions to use AWS resources in your account. 
    - This is useful if your organization already has its own identity system, such as a corporate user directory. It is also useful if you are creating a mobile app or web application that requires access to AWS resources.

    - When you use an IAM identity provider, you don't have to create custom sign-in code or manage your own user identities. The IdP provides that for you. Your external users sign in through a well-known IdP, such as Login with Amazon, Facebook, or Google. You can give those external identities permissions to use AWS resources in your account. IAM identity providers help keep your AWS account secure because you don't have to distribute or embed long-term security credentials, such as access keys, in your application.
- **Identity federation**
    - A method to delegate authentification of user to a trusted external system 
    - Organizations typically have a central identity provider or "IdP" that they use to store and authenticate their internal users. When moving to AWS, they regularly choose to continue using their IdP. In these cases, users can be given access to AWS through identity federation
    - And *unlike AWS SSO*, access needs to be configured separately within each account.

## AWS SSO
> AWS Single Sign-On, also known as AWS SSO, is a service that assists in providing one central location to manage identities and access to multiple AWS accounts and business applications.


- [SSO faqs](https://aws.amazon.com/ko/single-sign-on/faqs/)


## Week 1 Assessment and Discussion (7/7)
> [Week1 Quiz](https://learning.edx.org/course/course-v1:AWS+AWS-OTP-AWSD13+3T2020/block-v1:AWS+AWS-OTP-AWSD13+3T2020+type@sequential+block@869e2d1c59534ff1a90b554f6e6974bc/block-v1:AWS+AWS-OTP-AWSD13+3T2020+type@vertical+block@f50249ab0a284b42ad551eca7587b92f)

## Quiz1
- Which of the following best defines authentication?
    - The process of verifying a user’s permissions.
    - **The process of validating a user’s identity.**
    - The validation of a user’s identity and verification of their permissions
    - The process of protecting your personal information as data is transferred
## Quiz2
- Which of the following is a true about IAM roles?
    - IAM roles are considered long-term credentials.
    - You should rarely use roles as an authentication method.
    - Roles are associated with a specific person or machine.
    - **Roles are assumed by users and services when they need short term credentials.**
## Quiz3
- True or false: Amazon EC2 instances are virtual servers that can be resized on demand. (True)

## Quiz4
- Which is NOT one of the 4 prompts you see when configuring the AWS Command Line Interface?
    - AWS Access Key ID
    - AWS Secret Access Key
    - **Default Availability Zone**
    - Default output format
    - Default Region name
## Quiz5
- What is the maximum bucket size of Amazon Simple Storage Service?
    - 5GB
    - 50GB
    - 5TB
    - 500TB
    - **Unlimited**
## Quiz6
- What is the term for an external user trusted in AWS through identity federation?
    - Outside identity
    - **Federated identity**
    - External user
    - Federated external
## Quiz7
- AWS Identity and Access Management policies are used to define permissions for what kind of operation methods?
    - API calls made through an SDK
    - AWS Command Line Interface
    - AWS Management Console operations
    - **All of the above**

