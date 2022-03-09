---
title: "[Clean Code] Chapter 9: Unit Tests"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---


# DAY8 : Chapter9 Unit Tests
#### 오늘읽은 범위: ~ 9장. 단위테스트



## 책에서 기억하고 싶은 내용

> **테스트 코드는 실제코드 못지 않게 중요하다. 테스트코드는 이류시민이 아니다. 테스트 코드는 실제 코드 못지 않게 깨끗하게 짜야한다.**



- 코드에 유연성 유지보수성 재사용성을 제공하는 버팀목은 Unit Test
- 깨끗한 테스트 코드를 만들려면? 세가지가 필요하다
    - **가독성, 가독성, 가독성** 
    - 어쩌면 가독성은 실제코드보다 테스트 코드에서 더더욱 중요하다. 

- 숙련된 개발자라면 자기 코드를 좀 더 간결하고 표현력이 풍부한 코드로 리펙터링해야 마땅하다.
- Unit Test 하나당 Concept 하나!

- **FIRST** 
    - Fast : 테스트는 빨리 돌아야한다.
    - Independent : 각 테스트는 서로 의존하면 안된다.
    - Repeatable : 테스트는 어떤 환경에서도 반복가능해야한다. 실제 환경, QA환경, 로컬 환경드 테스트가 돌아가지 않는 환경이 하나라도 있다면 테스트가 실패한 이유를둘러댈 변명만 생긴다.
    - Self-Validating : 자가검증 (테스트는 BOOL값으로 결과를내야한다. 통과여부를 알려고 로그파일을 읽게 해서는 안된다. 테스트가 스스로 성공과 실패를 가늠하지 않는다면 판단은 주관적이되며 지루한 수작업평가가 이루어진다.)
    - Timely : 테스트는 적시에 작성해야한다. 단위테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다.
    - Test should be Fast

    - Tests should be Independent of other tests

    - Tests should be Repeatable in any environment

    - Tests should be Self-validating, having a boolean value: pass or fail

    - Tests should be written in Timely fashion

## 소감
- Unit test code 구현시에 실제 product code를 구현하는 것과같은 중요성이있다는 마음가짐으로 구현해야겠다.

## 궁금한 점 
- **TDD**
    - Test Driven Development
    - 테스트 주도 개발: 테스트가 개발을 이끌어 나간다.
    - 테스트를 먼저 만들고 테스트를 통과하기 위한 것을 짜는 것 즉, 만드는 과정에서 우선 테스트를 작성하고 그걸 통과하는 코드를 만들고를 반복하면서 제대로 동작하는지에 대한 피드백을 적극적으로 받는 것이다.



`#노마드코더`  
`#북클럽`  
`#노개북` 
