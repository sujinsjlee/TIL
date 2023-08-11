---
title: "[Google Cloud] Calling Cloud Functions from other functions"
categories:
  - GCP
tags:
  - GCP
---

> [GCP - Calling Cloud Functions from other functions](https://www.educative.io/answers/calling-cloud-functions-from-other-functions)

**Cloud Functions** is a serverless computing service provided by Google Cloud. It supports programming languages such as Node.js, Python, Go, Java, and .NET. In programming, a function is a unit of code that performs a specific task and can be reused throughout the program. Just like a function in a program, when an event occurs, Cloud Functions is triggered, and the specific code is executed accordingly. There is no need to provision or manage servers with Cloud Functions.  

Generally, a developer manages server provisioning in cloud computing systems, but with Google Cloud Functions, a developer only needs to write source code. Cloud automatically configures the necessary underlying infrastructure and executes and terminates the code. Cloud Functions only charges users for the time when the code is running.  

Cloud Functions offer a versatile set of capabilities that can address various use cases. These functions can automate various tasks, including resizing images, converting files, and transforming data. They are also ideal for data stream processing, enabling real-time analysis of data as it flows through your system. Additionally, Cloud Functions can integrate with different APIs, allowing us to seamlessly automate workflows and exchange data between various services.    

## What is serverless?
Serverless does not mean a backend without a server. Serverless refers to a backend without server management. In a traditional server-based system, the server must always be running and ready to respond to requests, even with no current workload. This can result in unnecessary costs and resource consumption. In a serverless architecture, developers upload functions are "asleep" until a request triggers their execution. When a request occurs, the Cloud Function wakes up the corresponding function and performs the requested operation. Once the operation is complete, the function returns to "sleep" until the subsequent request arrives.  

## How to trigger the event
The developer sets up Cloud Functions to execute in response to various scenarios by specifying a trigger for the function. A trigger can be one of many supported events:  

- HTTP triggers:
    - Incoming HTTP(S) requests.
- Event triggers:
    - Messages coming from the Pub/Sub message cue.
    - Events triggered by the Firebase Mobile SDK.
    - The Google Cloud Storage service creates, modifies, or deletes a file.

## Calling Cloud Functions

To call a Cloud Function inside another Cloud Function, create a Pub/Sub topic and send a message to its triggering Pub/Sub topic to trigger it. Pub/Sub is a messaging service that allows services to communicate asynchronously. Pub/Sub creates event producers and consumers, called publishers and subscribers. Publishers communicate with subscribers asynchronously by broadcasting events rather than synchronous remote procedure calls (RPCs).