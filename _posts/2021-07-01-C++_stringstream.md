---
title: "C++ - stringstream"
categories:
  - C++
tags:
  - C++
---

## std::basic_stringstream

> [std::basic_stringstream](https://en.cppreference.com/w/cpp/io/basic_stringstream)


- The class template **std::basic_stringstream** implements input and output operations on string based streams. It effectively stores an instance of std::basic_string and performs the input and output operations on it.

- C++에서 stringstream은 주어진 문자열에서 필요한 자료형에 맞는 정보를 꺼낼 때 유용하게 사용된다. stringstream에서 공백과 '\n' 을 제외하고 문자열엣 맞는 자료형의 정보를 빼낸다.

- Example

```c++
#include <iostream>
#include <iomanip>
#include <sstream>
 
int main()
{
    std::string input = "41 3.14 false hello world";
    std::istringstream stream(input);
    int n;
    double f;
    bool b;
 
    stream >> n >> f >> std::boolalpha >> b;
    std::cout << "n = " << n << '\n'
              << "f = " << f << '\n'
              << "b = " << std::boolalpha << b << '\n';
 
    // extract the rest using the streambuf overload
    stream >> std::cout.rdbuf();
    std::cout << '\n';
}
```

- Output
n = 41  
f = 3.14  
b = false  
hello world  