---
title: "[Clean Code] Chapter 2: Meaningful Names"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY2 : Chapter2 Meaningful Names
#### 오늘읽은 범위: ~ 2장.의미있는 이름

- 이름을 너무 simple하게 적지 말고 구체적인 의도를 분명히 밝혀라
- 일관성이 떨어지는 정보는 그릇된 정보다
- 읽는 사람이 차이를 알도록 이름을 지어라
- grep 하기 쉽게 이름을 지어라
- 클래스 이름과 객체이름은 명사
- 메서드 이름은 동사

## 책에서 기억하고 싶은 내용
> **좋은 이름으로 바꿔주면 오히려 반갑고 고맙다. 코드를 개선하려는 노력을 중단해서는 안된다.**  


### 의도를 분명히 밝혀라
- p22
    - **Use Intention-Revealing Names**

    ```c
    //---DON't
    int d; 
    //---DO
    int elapsedTimeInDays;
    int fileAgeInDays;
    ```

    ```c
    //---DON't
    List<int[]> list1 = new ArrayList<int[]>();
    for(int[] x : theList) {
        if(x[0] == 4) {
            list1.add(x);
        }
        return list1;
    } 
    ```

    ```c
    //---DO
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for(int[] cell : gameBoard) {
        if(cell[STATUS_VALUE] == FLAGGED) {
            flaggedCells.add(cell);
        }
        return flaggedCells;
    }   
    ```
### 그릇된 정보를 피하라
- p24
    
    - **Avoid Dis-information** : You should avoid the names that give clue or incorrect meanings.
    - 일관성이 떨어지는 정보는 그릇된 정보다

### 의미있게 구분하라
- p25
    - **Make Meaningful Distinctions**
    - 읽는 사람이 차이를 알도록 이름을 지어라
    
    ```c
    //---DON'T
    class Customer {

    }
    class CustomrerInfo {

    }
    ```

### 발음하기 쉬운 이름을 사용하라
- p27
    - **Use Pronounceable Names**

### 검색하기 쉬운 이름을 사용하라
- p28    
    - **Use Searchable Names**

    
    ```c
    //---DON't
    for(int i = 0; i <34; i++) {
        s += t[i] * 4;
    }
    //---DO
    const int NUMBER_OF_TASKS = 34;
    const int WORK_DAYS_PER_WEEK = 5;
    int sum = 0;
    for(int j = 0; j < NUMBER_OF_TASKS; j++) {
        int realTaskDays = taskEstimate[j] * realDaysPerIdearday;
        int realTaskWeeks = realTaskDays / WORK_DAYS_PER_WEEK;
        sum += realTaskWeeks;
    }

    ```


### 클래스 이름과 객체이름은 명사
### 메서드 이름은 동사
- p30
    - Should be **verb or verb phrase** like postPayment, deletePage, or save.
    - Should be **noun or noun phrase** like Customer, Account, or AddressParser.
    - Avoid words like **Manager, Processor** in the name of the class, because it's means that the class do more than one thing and this indicates to a God Class (this thing should avoid).

### 한 개념에 한 단어를 사용하라
- p33
    - Pick One Word per Concept


## 소감
- **Avoid Encoding** 
    - 멤버변수에 `m_` 있는게 가독성이 좋다고 생각했는데, 클래스/함수가 간단하고 명확한경우 멤버변수에 `m_`을쓰는 것을 지양하자고한다. 나도 이부분을 기억하고 복잡하지 않은 경우는 사용하지 말아야겠다.
    - 추가적으로 인터페이스선언할때 `interface IShape` 이런식으로 I달지 말라는 코멘트가 있었다. 이런 코드를 거의 본 적이 없어서 몰랐었는데 주의해야겠다.
    - Interfaces and Implementations: If you want to create an Abstract Factory for the creation of shapes, this will be interface implemented by concrete class, so don't use IShapeFactory, because I don’t want the users knowing that I’m handing them by an interface. 

- 헝가리식 표기법
    - 변수 및 함수의 인자 이름 앞에 데이터 타입을 명시하는 코딩 규칙. 하지만 공식 가이드 라인에서는 사용하지 말 것을 권고
    
`#노마드코더`  
`#북클럽`  
`#노개북` 