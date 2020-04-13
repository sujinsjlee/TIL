---
title: "C++ [STL] 반복자"
categories:
  - C++
tags:
  - C++
published: false
---

## 반복자
복합 개체의 내부구조에 상관없이 순차적으로 요소에 접근하기 위한 방법을 제공하는 것  
Provide a way to access the elements of an aggregate object sequentially without exposing its undelying representation.  

## 반복자 (iterator) in STL
> ++연산자로 이동이가능하고, *연산자로 요소에 접근이 가능한 것

* 반복자의 형태
	* Raw Pointer
	* 컨테이너의 요소를 열거하기 위한 객체(beding())
	* 스트림 반복자 (stream iterator)
	* 삽입 반복자 (insert iterator)
	
## 핵심 
1. 반복자 타입
> 컨테이너 이름 <요소타입> ::iterator  
> C++11 부터는 auto 사용  

2. 반복자를얻는 방법
* 멤버 함수 사용: begin(), end()
* 일반함수 사용 :  STL 컨테이너 뿐 만 아니라 배열도 사용가능 (from C++11)

```cpp


#include <iostream>
#include <list>   
#include <vector>
using namespace std;

int main()
{
	list<int> s = { 1,2,3,4,5 };
	//vector<int> s = { 1,2,3,4,5 };

	//int s[5] = { 1,2,3,4,5 };
	
	//list<int>::iterator p = s.begin();

	//auto p1 = s.begin();  // 배열은 error, STL 멤버함수사용법

	auto p1 = begin(s); // STL container 와 배열

	int n = size(s); //  s.size();
	cout << n << endl;

}

```