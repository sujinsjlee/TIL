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

