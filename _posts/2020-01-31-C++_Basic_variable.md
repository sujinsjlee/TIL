---
title: "C++ [Basic] 변수"
categories:
  - C++
tags:
  - C++
---

## C++ 변수의 특징
1. 구조체를 만들 때 **멤버를 초기화** 할 수 있다. (from C++11)  
C++98, 03에서는 멤버를 초기화하지않고 선언하면 0으로 초기화됨  
2. uniform intialization  
변수를 초기화 할 때 **중괄호 {} 를 사용해서 초기화**  
3. **auto / decltype**  
변수의 타입을 <u>컴파일러</u>가 결정하는 문법  
```c++
int x[5] = {1,2,3,4,5};

auto n1 = x[0];
decltype(n1) n3;
```
* **auto**  
	* **우변의 수식으로 좌변의 타입**을 결정  
	* 반드시 **초기값**이 필요  
	* 우변이 배열이면 **요소를 가리키는 포인터 타입**으로 타입이 결정    
* **decltype**   
	* **()안의 표현식**을 가지고 타입을 결정  
	* 초기값이 없어도 됨  
	* ()안의 표현식이 배열이면 **()안의 표현식과 완전 동일한 배열 타입**으로 타입 결정  
  ```c++
  int main()
  {
      int n1 = 10;
      
      auto a1 = n1;       // int
      decltype(n1) d1;    // int  

      int x[3] = { 1,2,3}; // int[3]

      auto a2 = x;  // 1. int a2[3] = x; 라고 추론하면 error
                    // 2. int* a2 = x;   라고 추론하면 ok.
      
      decltype(x) d2;  // int d2[3]  로 추론..
      // decltype(x) d3 = x; //   int d3[3] = x; 컴파일 에러 
      
      int y[2] = {1,2};
      
      auto a4 = y[0]; // int
      
      decltype(y[0]) d4; // int 가 아니고 int&

  }
  ```  
* decltype과 함수 호출식  
	* decltype(함수이름) : 함수타입  
	* decltype(&함수이름) : 함수 포인터 타입  
	* decltype(함수호출식) : 함수 반환 타입 (실제로 함수가 호출되는 것은 아님)  
  ```c++
  #include <iostream>
  #include <typeinfo>

  int foo(int a, double d)
  {
      return 0;
  }

  int main()
  {
      foo(1, 3.1);
      
      decltype( foo )  d1; // 함수 타입 - int(int, double)
      decltype( &foo ) d2; // 함수 포인터 타입- int(*)(int, double)
      decltype( foo(1, 3.1) ) d3; // 함수 반환 타입 - int
      
      std::cout << typeid(d1).name() << std::endl;
      std::cout << typeid(d2).name() << std::endl;
      std::cout << typeid(d3).name() << std::endl;
      
      const int c = 0;
      std::cout << typeid(c).name() << std::endl; // const, reference는 출력 안됨      
  }
  ```  
4. using  
* using 
	* 기존 타입의 별칭을 만들 때 사용  
	* C++11 부터 도입
* using vs. typedef  
	* typedef 는 **타입의 별칭**만 만들 수 있다
	* using은 타입뿐만 아니라 **템플릿의 별칭**도 만들 수 있다  
  ```c++
  //typedef int DWORD;
  //typedef void(*F)(int, int);

  using DWORD = int;
  using F = void(*)(int, int);


  int main()
  {
      DWORD n; // int n
      F f;     // void(*f)(int, int)
  }
  ```  
5. constexpr  
* **컴파일 시간에 결정되는 상수 값**으로만 초기화 (C++11 도입)  
* const vs. constexpr  
	* const  
		* 컴파일 시간 상수와 실행 시간 상수를 모두 만들 수 있다  
		* 변수 값으로 초기화 할 수 있다
	* constexpr  
		* **컴파일 시간 상수**만 만들 수 있다  
		* 컴파일 시간에 계산될 수 있는 값으로만 초기화가능  
		* 템플릿 인자로 사용될 수 있다  
* 따라서 변수값으로 초기화하는 경우가 아니라면 constexpr을 사용하여 최적화시켜야  
```c++
constexpr double pi = 3.14;

int main()
{
    int n = 10;
    
    const int c1 = 10; // 컴파일 시간 상수. 배열 크기
    const int c2 = n;  // 실행시간 상수. cl 컴파일러 기준으로 배열 크기 안됨..
    
    constexpr int c3 = 10; // ok
    constexpr int c4 = n; // error
    
}
```
{: .notice}


* C언어와 배열의 크기  
	* C89
		* 컴파일 시간에 크기를 알 수 있어야함  
	* C99
		* 배열의 크기로 변수도 사용가능  
		* g++은 지원하지만 cl컴파일러는 지원하지 않는다.
	```c++
	int arr1[10]; //ok
	
	int s1 = 10;  
	int arr2[s1]; //g++ :ok, cl: error  
	```
{: .notice--warning}