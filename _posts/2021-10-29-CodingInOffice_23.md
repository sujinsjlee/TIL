---
title: "[ETC] Sharing comment"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

- 시퀀스 설명할때 **function call**이랑 **메시지 보내는것**은 다르고 듣는사람 헷갈릴 수 있으니까 조심할 것
  - `2021.10.29`
  - `2022.01.19`
    > **What is callback function?**  
    > [A Callback function](https://stackoverflow.com/questions/824234/what-is-a-callback-function)  

    
    - **A callback function is a function which is:**
      - **passed as an argument to another function, and,**
      - **is invoked after some kind of event.**
  - In computer programming, a callback, also known as a "call-after"[1] function, is any executable code that is passed as an argument to other code; that other code is expected to call back (execute) the argument at a given time. This execution may be immediate as in a synchronous callback, or it might happen at a later point in time as in an asynchronous callback. 
  - 호출될 함수를 알려 주어 다른 프로그램 또는 다른 모듈에서 함수를 호출하게 하는 방법. 일반적으로 OS가 호출할 application의 함수를 지정해 특정한 event 또는 message가 발생했을 때 호출되도록 지정할 수 있다. 이런 함수를 callback함수라도 함






- [why file include is not recommended in header file](https://stackoverflow.com/questions/2596449/including-includes-in-header-file-vs-source-file)

- Generally, you only want to put the minimum necessary includes into a class header file, as anyone else who uses that header will be forced to `#include` all of them too. In larger projects, this leads towards slower builds, dependency issues, and all sorts of other nastiness.

- *메타데이터(metadata)* : Contrtucted data with purpose (Metadata is "data that provides information about other data", but not the content of the data, such as the text of a message or the image itself.)

- *페이로드(payload)*는 전송되는 데이터를 의미합니다. 데이터를 전송할 때, 헤더와 메타데이터, 에러 체크 비트 등과 같은 다양한 요소들을 함께 보내어, 데이터 전송의 효율과 안정성을 높히게 됩니다. 이 때, 보내고자 하는 데이터 자체를 의미하는 것이 바로 페이로드입니다. 우리가 택배 배송을 보내고 받을 때, 택배 물건이 페이로드이고, 송장이나 박스, 뾱뾱이와 같은 완충재 등등은 부가적인 것이기 때문에 페이로드가 아닙니다.
