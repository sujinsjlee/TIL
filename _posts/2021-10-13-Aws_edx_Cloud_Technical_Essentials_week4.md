---
title: "AWS - AWS Cloud Technical Essentials_week4"
categories:
  - AWS
tags:
  - AWS
---

> **Work hard, have fun, and make history.**  
> [AWS Cloud Technical Essentials](https://www.edx.org/course/aws-cloud-technical-essentials)  


# AWS Cloud Technical Essentials - Week4

## Monitoring on AWS
- **Amazon CloudWatch**
    - AWS resources create data you can monitor through metrics, logs, network traffic, events, and more. This
    - Amazon CloudWatch is a monitoring and observability service that collects data like those mentioned in this module. 
    - Detect anomalous behavior in your environments.
    - Set alarms to alert you when something’s not right.
    - Visualize logs and metrics with the AWS Management Console.
    - Take automated actions like scaling.
    - Troubleshoot issues.

## Introduction to Amazon CloudWatch
- **How CloudWatch Works**
    - CloudWatch acts as one centralized place where metrics are gathered and analyzed
    - Different AWS resources post different metrics that you can monitor. You can view a list of services that send metrics to CloudWatch in the resources section of this unit.
    - *basic monitoring* 
        - Many AWS services send metrics automatically for free to CloudWatch at a rate of one data point per metric per 5-minute interval, without you needing to do anything to turn on that data collection. 
    - *detailed monitoring*
        - you can get more granularity by posting metrics every minute using a feature like detailed monitoring. 
        -  Detailed monitoring has an extra fee associated

- **Break Down Metrics**
    - Each metric in CloudWatch has a timestamp and is organized into containers called *namespaces*. Metrics in different namespaces are isolated from each other—you can think of them as belonging to different categories.

- **Set Up Custom Metrics**
    - Custom metrics allows you to publish your own metrics to CloudWatch.
    - If you want to gain more granular visibility, you can use high-resolution custom metrics, which enable you to collect custom metrics down to a 1-second resolution.

- **Learn the CloudWatch Logs Terminology**
    - *Log event*: A log event is a record of activity recorded by the application or resource being monitored, and it has a timestamp and an event message.
    - *Log stream*: Log events are then grouped into log streams, which are sequences of log events that all belong to the same resource being monitored. 
    - *Log groups*: Log streams are then organized into log groups. A log group is composed of log streams that all share the same retention and permissions settings.

- **Configure a CloudWatch Alarm**
    - An alarm has three possible states.
        - *OK*: The metric is within the defined threshold. Everything appears to be operating like normal.
        - *ALARM*: The metric is outside of the defined threshold. This could be an operational issue.
        - *INSUFFICIENT_DATA*: The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state.

## Route Traffic with Amazon Elastic Load Balancing
- **What’s a Load Balancer?**
    - Load balancing refers to the process of distributing tasks across a set of resources.
    - It’s time to distribute the requests across all the servers hosting the application using a load balancer.
    - Although it is possible to install your own software load balancing solution on EC2 instances, AWS provides a service for that called *Elastic Load Balancing (ELB)*.

- **Features of ELB**
    - It can distribute incoming application traffic across EC2 instances as well as containers, IP addresses, and AWS Lambda functions.
    - ELB is highly available. The only option you have to ensure is that the load balancer is deployed across multiple Availability Zones.
    - In terms of scalability, ELB automatically scales to meet the demand of the incoming traffic. 

- **ELB Components**
    - *Listeners* : The client connects to the listener. This is often referred to as client-side.
    - *Target groups* : The backend servers, or server-side, is defined in one or more target groups. This is where you define the type of backend you want to direct traffic to, such as EC2 Instances, AWS Lambda functions, or IP addresses. 
    - *Rules* :  To associate a target group to a listener, a rule must be used. Rules are made up of a condition that can be the source IP address of the client and a condition to decide which target group to send the traffic to.

- **ELB Types**
    - *Application Load Balancer (ALB)*
        - Layer7 : HTTP/HTTPS
        - Send responses directly to the client. ALB has the ability to reply directly to the client with a fixed response like a custom HTML page.
    - *Network Load Balancer (NLB)*
        - Layer4 : TCP/UDP/TLS
        - Network Load Balancer supports TCP, UDP, and TLS protocols.
    - *Gateway Load Balancer*
        - Layer3+4:IP

## Amazon EC2 Auto Scaling

- **Differentiate Between Traditional Scaling and Auto Scaling**
    - It’s important to turn off the unused services, especially EC2 instances that you pay for On-Demand.
    - The need here is for a tool that automatically adds and removes EC2 instances according to conditions you define—that’s exactly what the EC2 Auto Scaling service does.

- **Use Amazon EC2 Auto Scaling**
    - The EC2 Auto Scaling service works to add or remove capacity to keep a steady and predictable performance at the lowest possible cost. By adjusting the capacity to exactly what your application uses, you only pay for what your application needs.

- **Configure EC2 Auto Scaling Components(what/where/when)**
    - *Launch template or configuration*: `What resource` should be automatically scaled?
    - *EC2 Auto Scaling Group*: `Where` should the resources be deployed?
    - *Scaling policies*: `When` should the resources be added or removed?

- **Get to Know EC2 Auto Scaling Groups**
    - EC2 Auto Scaling Group (ASG) enables you to define where EC2 Auto Scaling deploys your resources. 

[Exercise 7: Configure High Availability for your Application](https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/lab-7-elb.html)

## Week 4 Assessment and Discussion (6/7)
> [Week4 Quiz](https://learning.edx.org/course/course-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@sequential+block@ffcfefbe99e74e33a62a349d10f62edf/block-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021+type@vertical+block@a3d0832fbdca4176973f1a7a2fc983d0)  


### Question 1 
- What are the three components of EC2 Auto Scaling?
    - Scaling policies, security group, EC2 Auto Scaling group
    - Launch template, scaling policies, EC2 Auto Scaling group
    - Security group, instance type, Key pair
    - AMI ID, instance type, storage
<!--correct
Answer
Correct:EC2 Auto Scaling requires you to specify three main components: a launch template or a launch configuration as a configuration template for the EC2 instances, an EC2 Auto Scaling group that allows you to specify your minimum, maximum, and desired capacity of your instances, and scaling policies that allow you to configure a group to scale based on the occurrence of specified conditions or on a schedule. This information can be found in the video “Amazon EC2 Auto Scaling”.-->


### Question 2 (X) 
- Elastic Load Balancing includes which of these features?
    - A) Automatic scaling
    - B) AI for categorizing employee photos
    - C) Integration with Auto Scaling
    - A and B
    - A and C
<!--incorrect
Answer
Incorrect:ELB automatically scales depending on the traffic. It handles the incoming traffic and sends it to your backend application. ELB also integrates seamlessly with EC2 Auto Scaling. As soon as a new EC2 instance is added to or removed from the EC2 Auto Scaling group, ELB is notified and can begin to direct traffic to the new instance. This content is covered in “Route Traffic with Amazon Elastic Load Balancing”.-->

### Question 3
- True or false: When you use Elastic Load Balancing with your Auto Scaling group, it's not necessary to register individual EC2 instances with the load balancer.
    - True
    - False
<!--correct
Answer
Correct:Instances that are launched by your Auto Scaling group are automatically registered with the load balancer. Likewise, instances that are terminated by your Auto Scaling group are automatically deregistered from the load balancer. Check out Reading 4.5 for more information.-->

### Question 4
- Which of the following ELB load balancer types should be used for an application requiring to choose target groups with a rule based on the domain of a website?
    - Classic Load Balancer
    - Application Load Balancer
    - Network Load Balancer
    - Target Load Balancer
<!--correct
Answer
Correct:Application Load Balancer is a layer 7 load balancer that routes HTTP and HTTPs traffic, with support for rules. Due to this, Application Load Balancer is the correct choice for this application.This content is covered in “Route Traffic with Amazon Elastic Load Balancing”.-->

### Question 5
- What are the two ways that an application can be scaled?
    - Vertically and horizontally
    - Diagonally and vertically
    - Horizontally and diagonally
    - Independently and vertically
<!--correct
Answer
Correct:An application can be scaled vertically by adding more power to an existing machine or it can be scaled horizontally by adding more machines to your pool of resources. This information is found in the video “Optimizing Solutions on AWS”.-->

### Question 6  
- Dashboards contain different elements that allow you to view/analyze metrics called:
    - Widgets
    - Graphs
    - Icons
    - Components
<!--correct
Answer
Correct:AWS calls the elements you can add to a Dashboard widgets. Read more here: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create-and-work-with-widgets.html. This information can be found in the Introduction to Amazon CloudWatch video.-->

### Question 7 
- A metric alarm has what following possible states?
    - OK, ALARM, NOT_AVAILABLE
    - OK, ALERT, INSUFFICIENT_DATA
    - OK, ALARM, INSUFFICIENT_DATA
    - OK, ALERT, NOT_AVAILABLE
<!--correct
Answer
Correct:A metric alarm has the following possible states: OK – The metric or expression is within the defined threshold. ALARM – The metric or expression is outside of the defined threshold. INSUFFICIENT_DATA – The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state. Read more here: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html This information can be found in the Introduction to Amazon CloudWatch video.-->

[Course End](https://learning.edx.org/course/course-v1:AWS+AWS-AWS-OTP-AWSD16+1T2021/course-end)
