---
title: "C++ - preprocessor"
categories:
  - C++
tags:
  - C++
---

## preprocessor 전처리문

```c++
#include<bits/stdc++.h>
using namespace std;

#define NUM 10
#define STR "String"
#define SUM(x,y) ((x) + (y)) // define 으로 macro 만들기

//#undef NUM

void main()
{
  
  cout << NUM;
  cout << STR;
  cout << SUM(2,4);
  
#if NUM <40
  cout << "under 40" <<endl;
#elif NUM > 40
  cout << "exceed 40" << endl;
#else
  cout << NUM << endl;
#endif

}
```

- 코드가 실행되는 과정
    - **전처리기** > 컴파일러 > 링커 > 실행파일 생성
    - 컴파일전에 실행되는 부분이 preprocessor

- 전처리문은 앞에 **#**을 붙인다.
- 전처리문 끝에 **;** semicolon을 붙이지 않는다

### define 
- `#define` 키워드 내용 : 내용을 키워드로 사용할 수 있게 선언
- macro에 활용됨 
  - macro 선언할 때 연산자 우선순위 고려하여 괄호 처리

### undef 
- `#undef` : #define으로 선언된 키워드를 삭제


```c++
#include<bits/stdc++.h>
using namespace std;

#define NUM 40

void main()
{
#ifdef NUM
  cout << NUM << "is exist" << endl;
#else 
  cout << NUM << "is not exist" << endl;
#endif
}
```

### ifdef
- `#ifdef` : 키워드가 #define문으로 선언되어있으면 참


```c++
// header.h

#ifndef _TEST_H_
#define _TEST_H_
/// test code
#endif
```

### ifndef
- `#ifndef`: 키워드가 #define문으로 선언되어있지 않으면 참
  - 중복정의를 막아줌 
    - avoid redefinition
    - avoid predefinition
  - EXAMPLE
    - **#ifndef _TEST_H_** : _TEST_H_ 키워드가 선언되어있는지 확인
    - **#define _TEST_H_** : _TEST_H_ 키워드가 없다면 _TEST_H_ 을 define 해줌
    - /// test code
    - #endif

    - 추후에 다시 해당 ///test code를 접근할때 
    - #ifndef _TEST_H_ 이 조건에 의해 이미 _TEST_H_ 가 정의되어있으므로 아래 define 문을 거치지 않게 됩니다.


```c++
// header.h

#pragma once
```

### pragma once
- `#pragma` 명령 : 명령에 따라 특수한 기능을 한다. 
- **컴파일러에 종속적** 
- **#pragma once** : 이 헤더파일은 한번만 include시켜라
