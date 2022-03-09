---
title: "[Clean Code] Chapter 10: Classes"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---


# DAY9 : Chapter10 Unit Tests
#### 오늘읽은 범위: ~ 10장. 클래스



## 책에서 기억하고 싶은 내용

> **CLASSES SHOULD BE SMALL**  
> **Isolating from Change (Loose Coupling – Dependency Invertion Principle)**


- public 변수가 필요한 경우는 거의 없다
- class는 작아야한다!
- SRP Single Responsibility Principle 
    - 클래스나 모듈은 변경할 이유가 단 하나만 있어야한다.
- High Cohesion
    - 클래스는 인스턴스 변수 수가 저거야한다.
    - 모든 인스턴수 변수를 메서드마다 사용하는 클래스는 응집도가 높다
    - 응집도가 높다는 말은 클래스에 속한 메서드와 변수가 서로 의존하며 논리적인 단위로 묶인다는 의미기 때문이다
- 변경하기 쉬운 Class
    - 새 기능을 수정하거나 변경 할 때 건드릴 코드가 최소인 시스템 구조가 바람직하다
    - **이상적인 시스템이라면 새 기능을 추가할때 시스템을 확장할 뿐 기존 코드를 변경하지는 않는다**
- 변경으로부터의 격리
    - 인터페이스와 추상클래스를 사용해 구현이 미치는 영향을 격리
 
## 소감
- 시스템에 새로운 기능을 추가할때 추가 구현 즉, 시스템확장을 고려하고 legacy 코드는 그대로 유지하는 것을 중요하게 생각하자



`#노마드코더`  
`#북클럽`  
`#노개북` 
