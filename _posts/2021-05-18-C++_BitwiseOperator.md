---
title: "C++ - Bitwise Operators"
categories:
  - C++
tags:
  - C++
---

## Bitwise Operators
- [c++ reference:Bitwise Operators](https://en.cppreference.com/w/cpp/language/operator_arithmetic)

## bitmask c++ 연산
- **비트마스크 (BitMask)란?**
	- 비트마스크는 이진수를 사용하는 컴퓨터의 연산 방식을 이용하여, 정수의 이진수 표현을 자료구조로 쓰는 기법
- **비트연산자**
	- AND : (**&**) 두 정수를 한 bit씩 비교하면서 해당 bit가 둘다 1인경우에 1
	- OR : (**|**) 두 정수를 한 bit씩 비교하면서 하나의 bit라도 1인 경우에 1
	- XOR : (**^**) 두 정수를 한 bit씩 비교하면서 하나의 bit만 1인경우에 1
	- NOT : (**~**) 정수하나를 입력받아서 한 비트씩 탐색하며 1인 bit는 0으로, 0인 bit는 1로 
	- Shit : (**<<**)/(**>>**) 비트들을 왼쪽 또는 오른쪽으로 원하는 만큼 움직이고 움직이고 나서 빈 자리는 0으로 채워진다.
	
	```c++
	// 13 - 00001101
	int bitmask1 = (13 << 1); // 00011010
    int bitmask2 = (13 >> 1); // 00000110
	cout << bitmask1 << endl; // 26
	cout << bitmask2 << endl; // 6


    do
    { 
        Vec.push_back( x & 1 )
    } 
    while ( x >>= 1 ); // x = (x >> 1)
	```

    - `x & 1` produces a value that is either 1 or 0, depending on the least significant bit of `x`: if the last bit is 1, the result of `x & 1` is 1; otherwise, it is 0. This is a `bitwise AND` operation.
