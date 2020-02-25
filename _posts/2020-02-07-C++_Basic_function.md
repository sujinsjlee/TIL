---
title: "C++ [Basic] 함수"
categories:
  - C++
tags:
  - C++
published: false
---
## C++ 함수  
### 1. Default parameter  
* 함수 호출시 인자를 전달하지 않으면 **미리 지정된 인자 값**을 사용  
* C 언어에는 없고 C++에서 도입된 문법  
* 주의사항  
    * 함수의 **마지막 인자부터 차례대로 디폴트 값을 지정**해야 함  
    * 함수의 **선언부**에만 디폴트 값을 표기  
    
### 2. function overloading 함수 오버로딩  
* C++ 에서는 C언어와 달리 동일한 이름의 함수를 여러개 만들 수 있음  
* 단, **인자의 개수나 인자의 타입**이 달라야함  
  * 인자의 개수가 달라도 **디폴트 값**이 있는 경우는 주의해야
  * 정수타입과 포인터 타입에 대한 오버로딩은 사용하지 않는 것을 권장
  ```c++
  void f(int n){}
  void f(char* s){}

  f(0);//compile ok-> f(int) will be called 
        //not recommended code
  f(nullptr); //f(char*) will be called
  ```
### 3. function template  
* template 의 기본 개념  
  * 타입만 다르고 구현이 동일하거나 유사한 함수가 있을 때, 컴파일러가 함수를 생성  
  * 컴파일러가 함수를 생성할 때 사용할 **함수의 틀 --> template**  
  ```c++
  template<typename T> //template parameter
  T square(T a) //call parameter
  {
    return a*a;
  }
  int main()
  {
      square<int>(3);
      square<double>(3.3);

      square(5);
  }
  ```
  * template parameter   
    * **컴파일 시간**에 전달되어서 함수가 생성
    * 함수가 생성되는 과정: **템플릿 인스턴스화(template intantiation)**  
    * template parameter를 표기할 때 "typename" 또는 "class" 키워드 사용 가능  
  * call parameter  
    * **실행시간**에 함수에 전달  
  * type deduction  
    * 함수템플릿 사용시 타입을 명시적으로 지정하지 않으면, **함수호출인자를 보고 컴파일러가 결정**  

* 클래스(구조체) 템플릿  
  * 함수뿐 아니라 클래스, 구조체도 템플릿으로 만들 수 있음  
  ```cpp
  template<typename T>
  struct Point
  {
      T x;
      T y;
  };

  int main()
  { 
      Point<int> pt;
      pt.x = 1;
      pt.y = 1;

      Point<double> pt2;
  }
  ```   

### 4. inline function  

### 5. delete function  

### 6. constexpr function  

### 7. lambda expression  