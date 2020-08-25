---
title: "[ETC] - C++ Concept"
publish:false
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---
<!--코딩잘하고싶다-->
## Concept 
- __Client__ : The originator of a request. The destinaction endpoint of a response.  
- __Server__ : The destination endpoint of a request. The originator of a response.  
- __Observer__ : A client that can register itself using a modified GET message. The observer is then connected to a resource, and if the state of that resource changes, the server will send a notification back to the observer.  
- __Provider__ : The provider is a server that processes the requests issued by clients.  
- __User__  
- __call__ __back__   
- __Endpoint__  


## Application Framework
- 프로세스 실행순서  
1. 전역변수 생성자. 기반 클래스 생성자
2. main 함수 실행

## Observer Pattern
- 객체 사이의 1:N 의 종속성을 정의하고 한 객체의 상태가 변하면 종속된 다른 객체에 통보가 가고 자동으로 수정이 일어나게 한다.  
- Obeserver 의 대상 : Subject  

