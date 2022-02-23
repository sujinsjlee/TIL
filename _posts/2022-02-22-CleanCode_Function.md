---
title: "[Clean Code] Chapter 3: Functions"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY3 : Chapter3 Functions
#### 오늘읽은 범위: ~ 3장.함수

- 작게 만들어라!
- 함수는 한 가지만 해야한다. 그 한 가지를 잘해야한다. 그 한 가지만을 해야한다.
- 코드는 위에서 아래로 이야기처럼 읽혀야 좋다
- 서술적인 이름을 사용하라
    - 이름이 길어도 괜찮다. 겁먹을 필요없다. 길고 서술적인 이름이 짧고 어려운 이름보다 좋다
- 함수인수에서 이상적인 인수개수는 0개이다
- 플래그 인수는 추하다!
- 함수이름 : 동사 + 인수 : 명사 + 함수이름에는 **키워드**가 있어야!
- if 조건문으로 오류코드추가하기보다 예외처리문 try-catch사용하기
- 중복제거! 반복하지마라!


## 책에서 기억하고 싶은 내용
> **함수를 어떻게 짜죠? 소프트웨어를 짜는 행위는 글짓기와 비슷하다. 먼저 생각을 기록한 후 읽기 좋게 다듬는다. 초안은 대개 서투르고 어수선하므로 원하는대로 읽힐때까지 말을 다듬고 문장을 고치고 문단을 정리한다. 처음부터 탁 짜내지 않는다. 그게 가능한 사람은 없으리라**  
  

> **master programmer는 시스템을 구현할 프로그램이 아니라 풀어갈 이야기로 여긴다. 프로그래밍 언어라는 수단을 활용해 더 풍부하고 표현력이 강한 언어를 만들어 이야기를 풀어간다**


- p47
    - 불행히도 swich 문은 N가지를 처리한다. 하지만 각 switch문을 반복하지 않기 위해서 polymorphism을 이용한다.
    
    ```java
    public abstract class Employee {
        public abstract boolean isPayDay();
        public abstract Money calculatePay();
        public abstract void deliveryPay(Money pay);
    }
    public interface EmployeeFactory {
        public Employee makeEmployee(EmployeeRecord r) throw InvalidEmployeeType;
    }
    public class EmployeeFactoryImpl implements EmployeeFactory {
        public Employee makeEmployee(EmployeeRecord r) throw InvalidEmployeeType {
            switch(r.type) {
                case COMMISSIONED:
                    return new CommissionedEmployee(r);
                case HOURLY:
                    return new HourlyEmployee(r);
                case SALARYIED:
                    return new SalariedEmployee(r);
                default:
                    throw new InvalideEmployee(r.type);
            }
        }
    }
    ```
- p50
    - 함수인수에서 이상적인 인수개수는 0개이다. 다음은 1개이고, 다음은 2개이다. 그 이상은 특별한 이유가 필요하다. 특별한 이유가 있어도 사용하면 안된다.
    - 인수가 3개가 넘어가면 갖가지 인수조합으로 함수를 검증하는 테스트 케이스를 작성하기가 상당히 부담스럽다
- p52
    - 플래그인수
    - 플래그인수는 추하다. 함수로 부울값을 넘기는 관례는 정말로 끔찍하다. 왜냐고? 함수가 한꺼번에 여러가지 일을 처리한다고 대놓고 공표하는 셈이니까!

- p53
    - 인수 2-3개가 필요하다면 일부를 독자적인 클래스 변수로 선언할 가능성을 짚어본다.

    ```c++
    //---DON't
    Circle makeCircle(double x, double y, double radius);
    //---DO
    Circle makeCircle(Point center, double radius);
    ```
- p58
    - try-catch블록은 원래 추하다. 코드 구조에 혼란을 일으키며 정상 동작과 오류처리 동작을 뒤섞는다. 그러므로 try-catch 문 내부내용을 별도 함수로 뽑아 내는 것이 좋다.

    ```c++
    public void delete(Page page) {
        try {
            deletePageAndAllReferences(page);
        }
        catch (Exception e) {
            logError(e);
        }
    }
    ```

## 소감
- try-catch 블록은 추하다! 이 부분의 원문을 찾아보니 "Try/catch blocks are ugly" 였다. ugly한 코드라니! 앞으로 짧고 간결하고 명확하게 함수를 구현할 수 있는 개발자가 되어야겠다. 

## 궁금한 점 
- **SRP** : Single Responsibility Principle
- **OCP** : Open Closed Principle
    - In object-oriented programming, the open–closed principle states "software entities should be open for extension, but closed for modification"; 
    - 기존의 코드를 변경하지 않으면서 기능을 추가할 수 있도록 설계
- polymorphism
    - 다형성(polymorphism)이란 하나의 객체가 여러 가지 타입을 가질 수 있는 것을 의미
    - Polymorphism in C++ means, the same entity (function or object) behaves differently in different scenarios.
    - In object-oriented programming, polymorphism (from the Greek meaning "having multiple forms") is the characteristic of being able to assign a different meaning or usage to something in different contexts - specifically, to allow an entity such as a variable, a function, or an object to have more than one form.

- 상속과 다형성의 주요 차이점 
    - 상속은 이미 존재하는 클래스에서 해당 기능을 파생시키는 클래스를 만드는 것입니다. 한편, 다형성은 여러 형태로 정의 할 수있는 인터페이스입니다.
    - 상속은 클래스에서 구현되지만, 다형성은 메소드 / 함수에서 구현됩니다.
    - 상속으로 인해 파생 클래스는 기본 클래스에 정의 된 요소와 메서드를 사용할 수 있으므로 파생 클래스는 이러한 요소를 정의하거나 다시 메서드를 요구할 필요가 없으므로 코드 재사용 가능성이 높아 지므로 코드 길이가 줄어 듭니다 . 반면 다형성을 사용하면 객체가 컴파일 타임과 런타임 모두에서 호출 할 메소드의 형식을 결정할 수 있습니다.
    - 상속은 단일 상속, 다중 상속, 다중 레벨 상속, 계층 적 상속 및 하이브리드 상속으로 분류 할 수 있습니다. 한편, 다형성은 오버로딩 및 오버라이드로 분류됩니다.
- 결론: 상속과 다형성은 상속 개념을 구현하는 클래스에 동적 다형성이 적용되므로 상호 관련된 개념입니다.



`#노마드코더`  
`#북클럽`  
`#노개북` 
