---
title: "Data Structure - (4) 스택"
categories:
  - Data Structure
tags:
  - Data Structure
link: https://mg729.github.io//datastructure/2020/01/12/DataStructure_(4)_Stack/
---

##  Stack (스택의 구조)
> **가장 나중에 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조**  
> stack은  <u>배열, 연결리스트</u>를 이용하여 구현

Last In First Out(LIFO)  

<ul>
 <li> push() : 데이터를 스택에 넣기 </li>
 <li> pop() : 데이터를 스택에서 꺼내기 </li>
</ul>

##  Stack 의 장단점
>stack 구현을 **배열**으로 했다고 가정하는 경우  

1. stack 의 장점  
* 구조가 단순, 구현이 쉽다.  
* 데이터 저장/읽기 속도가 빠르다  

2. stack의 단점  
* 데이터 최대 갯수를 미리 정해야한다.  
* 저장공간의 낭비가 발생할 수 있음 (최대 개수가 정해져있는데 그 공간을 모두 활용하지 않는 경우)  


##  Stack 과 Queue의 공통점 
> 데이터를 제한적으로 접근할 수 잇는 구조  
> 한쪽 끝에서만 데이터를 넣거나 뺄 수 있는 구조  

##  stack - C++ Container library  
[c++ stack](https://en.cppreference.com/w/cpp/container/stack).  
```c++
#include <iostream>
#include <stack>
using namespace std;

int main()
{
    stack<int> s1; 
	
    s1.push(10);
    s1.push(20);
    s1.push(30);
    
    cout << s1.top() << endl; //30
    
    s1.pop();
    
    cout << s1.top() << endl; //20
    
}
```

##  stack의 활용   
프로세스에서 함수 동작 방식 (함수 호출에 관여)  
스택 구조는 프로세스 실행 구조의 기본  