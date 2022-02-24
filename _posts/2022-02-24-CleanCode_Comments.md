---
title: "[Clean Code] Chapter 4: Comments"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY4 : Chapter4 Comments
#### 오늘읽은 범위: ~ 4장.주석 

- 주석으로 설명하려 애쓰는 대신에 코드를 깨끗이 명확히하는데 시간을 보내라
- 코드로 의도를 표현해라
- 예외적인 좋은 주석
    - 법적인 주석 // Copyright (C) ...
    - 정보를 제공하는 주석
    - 결과를 경고하는 주석
    - TODO 주석
    - 중요성을 강조하는 주석 // 아래 코드는 어떤 조건에서만 가능한 flow라든지.. 아니면 에러가 발생한다는 등의 중요 내용

## 책에서 기억하고 싶은 내용

> **나쁜 코드에 주석을 달지 마라, 새로 짜라.**  
  
- p68
    - 내가 이렇게 주석을 무시하는 이유가 무엇이냐고? 거짓말을 하니까. 주석은 오래될수록 코드에서 멀어진다. 오래될수록 완전히 그릇될 가능성도 커진다. 이유는 단순하다. **프로그래머들이 주석을 유지하고 보수하기란 현실적으로 불가능하니까**
    - 나라면 애초에 주석이 필요없는 방향으로 에너지를 쏟겠다.
    - 진실은 한곳에만 존재한다. 바로 코드다. 코드마니 정확한 정보를 제공하는 유일한 출처다. 그러므로 우리는 주석을 가능한 줄이도록 꾸준히 노력해야한다.

    ```c
    //---DON'T

    // Checkto see if the employee is eligible for full benefits
    if((employee.flags & HOURLY_FLAT) && (employee.age > 65)) {

    }
    //---DO
    if(employee.isEligibleForFullBenefits())
    ```
- p76
    - **나쁜 주석**
    - 주절거리는 주석
    - 같은 이야기를 반복하는 주석
    - 오해할 여지가 있는 주석
    - 코드 변경이력을 기록하는 주석
    - 있으나 마나한 당연한 사실을 언급하는 주석
    - 함수나 변수로 표현할 수 있다면 주석을 달지마라
    - 닫는 괄호에 다는 주석

    ```c
    //---DON'T
    try {

    } // while line is remained
    catch {

    }
    ```
    - 주석처리한 코드 --> 주석으로 처리된 코드는 다른 사람들이 지우기를 주저한다. 너가 지워라.
    - HTML 코드 
    - 너무 많은 정보
    - 주석과 코드사이의 모호한 관계


## 소감
- 함수이름과 변수명을 명확하게 naming하면서 주석을 줄이면서 코드를 구현해야겠다.

## 궁금한 점 
- Base64 인코딩이란?
    -  Base64란 Binary Data를 Text로 바꾸는 Encoding(binary-to-text encoding schemes)의 하나로써 Binary Data를 Character set에 영향을 받지 않는 공통 ASCII 영역의 문자로만 이루어진 문자열로 바꾸는 Encoding이다.


`#노마드코더`  
`#북클럽`  
`#노개북` 
