---
title: "[Clean Code] Chapter 7: Error Hanling"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY7 : Chapter7 Error Hanling
#### 오늘읽은 범위: ~ 7장. 오류처리
- 오류 Log코드보다 예외를 던지는 편이 낫다

## 책에서 기억하고 싶은 내용

> **뭔가 잘못되면 바로 잡을 책임은 바로 우리 프로그래머에게 있다**

- try-catch-finally 문 부터 먼저 사용하라
- Provide Context with Exceptions
    - Use informative error messages and relativant exception parameters
- Define Exception Classes in Terms of a Caller’s Needs
    - How they are caught?
- Define the normal flow
    - Cleanly separate business logic from error handling
- Don’t Return Null
- Don’t Pass Null
    - NULL 을 반환하거나 전달하지 말자
    - NullException처리를 고려하기 전에 NULL값은 그냥 전달하지도 반환하지도말자 

## 소감
- trace 를 남기고 logging으로 abnormal 처리하는게 익숙했는데 앞으로 코드를 구현할때 Exception 처리하는 것을 우선적으로 고려해야겠다.


## 궁금한 점 
- [Does C++ support 'finally' blocks? (And what's this 'RAII' I keep hearing about?)](https://stackoverflow.com/questions/161177/does-c-support-finally-blocks-and-whats-this-raii-i-keep-hearing-about)
    - No, C++ does not support 'finally' blocks. 
- what is **finally** block?
    - JAVA 예외처리
    - try{} 구문을 실행 중에 예외가 발생하면 그 지점에서 실행을 중지하고 catch{} 구문이 실행된다. 
    - catch() 메서드 인자로 발생하는 예외 클래스를 인자를 주면 된다. 
    - **finally{}** 는 예외가 발생하든 안하든 반드시 실행되어야하는 작업이 있을 시 사용하는데 생략해도 된다.


    ```java
    try { /** 
    * 정상이라면 이 코드는 아무런 문제없이 블록의 시작부터 끝까지 실행된다. 
    * 하지만 경우에 따라 예외가 발생할 수 있다. 
    * 예외는 throw 문에 의해 직접적으로 발생할 수도 있고, 
    * 또는 예외를 발생시키는 메서드의 호출에 의해 발생할 수도 있다. */ 
    } 
    catch (e) { /** 
    * 이 블록 내부의 문장들은 오직 try 블록에서 예외가 발생할 경우에만 실행된다. 
    * 이 문장들에선 지역 변수 e를 사용하여 Error 객체 또는 앞에서 던진 다른 값을 참조할 수 있다. 
    * 이 블록에서는 어떻게든 그 예외를 처리할 수도 있고, 
    * 그냥 아무것도 하지 않고 예외를 무시할 수도 있고, 
    * 아니면 throw 를 사용해서 예외를 다시 발생시킬 수도 있다. */ 
    } 
    finally { /** 
    * 이 블록에는 try 블록에서 일어난 일에 관계없이 무조건 실행될 코드가 위치한다. 
    * 이 코드는 try 블록이 어떻게든 종료되면 실행된다. 
    * try 블록이 종료되는 상황은 다음과 같다. 
    * 1) 정상적으로 블록의 끝에 도달했을 때 
    * 2) break, continue 또는 return 문에 의해서 
    * 3) 예외가 발생했지만 catch 절에서 처리했을 때 
    * 4) 예외가 발생했고 그것이 잡히지 않은 채 퍼져나갈 때 */
    }
    ```


`#노마드코더`  
`#북클럽`  
`#노개북` 
