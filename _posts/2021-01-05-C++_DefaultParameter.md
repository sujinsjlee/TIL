---
title: "C++ - Default Parameter"
categories:
  - C++
tags:
  - C++
---

## deault parameter
디폴트 매개 변수(default parameter)는 기본값이 제공된 함수 매개 변수다. 사용자가 이 매개 변수의 값을 제공하지 않으면 기본값(default value)이 사용된다.

## Multiple default parameter
```c++
void printValues(int x=10, int y=20, int z=30)
{ std::cout << "Values: " << x << " " << y << " " << z << '\n'; }
```

함수는 디폴트 매개 변수(default parameter)를 여러 개 가질 수 있다.
매개 변수 x와 y에 대한 인수를 제공하지 않고는 매개 변수 z에 인수를 제공할 수 없다. C++가 `printValues(, , 3)`과 같은 호출 구문을 지원하지 않기 때문이다. 이는 다음과 같은 규칙 때문이다.

모든 default parameter는 **오른쪽부터** 지정해야 한다. 그래서 다음은 허용되지 않는다.
```c++
void printValue(int x=10, int y) //not allowed
```

