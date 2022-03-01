---
title: "[Clean Code] Chapter 6: Objects and Data Structures"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY6 : Chapter6 Formmating
#### 오늘읽은 범위: ~ 6장. 객체와 자료구조
- 객체는 동작을 공개하고 자료를 숨긴다. 그래서 기존 동작을 변경하지 않으면서 새 객체타입을 추가하기는 쉬운 반면, 기존 객체에 새 동작을 추가하기는 어렵다.
- 자료구조는 별다른 동작없이 자료를노출한다. 그래서 새 동작을 추가하기는 쉬우나, 기존 함수에 새 자료구조를 추가하기는 어렵다.


## 책에서 기억하고 싶은 내용

> **새로운 자료타입을 추가하는 유연성이 필요하면 객체가 더 적합하고, 새로운 동작을 추가하는 유연성이 필요하면 자료구조와 절차적인 코드가 더 적합하다**



- 자료 추상화 Data Abstraction
    - Abstraction means hiding implementation. 
- 자료/객체 비대칭성Data/Object Anti-Symmetry
    - **Objects**: hide their data (be private) and have functions to operate on that data.
    - **Data Structures**: show their data (be public) and have no functions.

    - Procedural code (code using data structures)
        - Makes it easy to add new functions without changing the existing data structures.
        - Makes it hard to add new data structures because all the functions must change.
    - OO code (code using object oriented)
        - Makes it hard to add new functions because all the existing classes must change.
        - Makes it easy to add new classes without changing existing functions.
    - So, the things that are hard for OO are easy for Procedural, and vice-versa.
    - Q: when OO code is more appropriate?
        - A. In any complex system, because we will having to add more data types rather than new functions.
    - Q: when procedural code is more appropriate?
        - A. on the other hand, when we’ll want to add new functions more rather than data types.

- 디미터 법칙 The Law of Demeter
    -  다른 객체가 어떠한 자료를 갖고 있는지 속사정을 몰라야 한다는 것을 의미
    - 자료구조라면 디미터 법칙을 거론할 필요가 없다.
        - 객체라면 내부 구조를 숨겨야 하므로 디미터 법칙을 지켜야 한다. 하지만 자료구조라면 당연히 내부 구조를 노출해야 하므로 디미터 법칙이 적용되지 않는다.
    
    ```c
    //---DON'T
    public void showData(Car car) {
        print(car.getOwner().getId().getLicenseInfo());
    }
    //---DO
    Owner owner = car.getOwner();
    Address ownerId = owner.getId();
    Street ownerStreet = ownerId.getLicenseInfo();
    ```



## 소감
- get__()->get__() 꼬리물기 식의 코드 구현을 앞으로는 주의하도록 해야겠다.


## 궁금한 점 
- 휴리스틱 heuristic (직관적인,경험적인,대충 어림짐작하기,눈대중으로 맞추기, 즉흥적으로 맞추기, 주먹구구식으로 맞추기)
    - A heuristic, or heuristic technique, is any approach to problem solving or self-discovery that employs a practical method that is not guaranteed to be optimal, perfect, or rational, but is nevertheless sufficient for reaching an immediate, short-term goal or approximation.

`#노마드코더`  
`#북클럽`  
`#노개북` 
