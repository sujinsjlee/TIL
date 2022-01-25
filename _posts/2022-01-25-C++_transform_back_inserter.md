---
title: "C++ - transform, back_inserter"
categories:
  - C++
tags:
  - C++
---

## std::transform

```c++
template< class InputIt,
          class OutputIt,
          class UnaryOperation >
OutputIt transform( InputIt first1,
                    InputIt last1,
                    OutputIt d_first,
                    UnaryOperation unary_op );
```

> **std::transform** applies the given function to a range and stores the result in another range, keeping the original elements order and beginning at d_first.

## std::back_inserter

> **back_inserter** is a convenient function template that constructs a std::back_insert_iterator for the container c with the type deduced from the type of the argument.  
> A **std::back_insert_iterator** which can be used to add elements to the end of the container c

### Example

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>  // std::transform()
#include <iterator>   // std::back_inserter()


using std::string;
using std::vector;
using std::cout;

// inputVec의 모든 요소에 순차적으로 2를 곱연산하여
// outputVec 컨테이너의 끝에 순차적으로 추가합니다.

int main(void)
{
   
   
    // 1 2 3 4 5
    vector<int> inputVec {1, 2, 3, 4, 5};

    // 10 10 10 10
    vector<int> outputVec(4, 10);
    // empty vector
    vector<int> outputVec2;

    /*
        1. inputVec의 [begin, end) 범위의 각 요소를 람다 함수의 인자 n에 전달합니다.
        2. 각 결과마다 outputVec
        ex) inputVec의 첫 요소인 1에 2를 곱하여 추가, 다음 요소인 2에 2를 곱하여 추가..
    */
    std::transform(inputVec.begin(), inputVec.end(), std::back_inserter(outputVec),
            [](int n) { return n*2; });

    // 10 10 10 10 2 4 6 8 10
    for (vector<int>::const_iterator iter = outputVec.begin(); iter != outputVec.end(); ++iter)
    {
        cout << *iter << " ";
    }

    cout << "\n";

    std::transform(outputVec.begin(), outputVec.end(), std::back_inserter(outputVec2),
            [](int n) { return n*2; });

    // 20 20 20 20 4 8 12 16 20
    for (vector<int>::const_iterator iter = outputVec2.begin(); iter != outputVec2.end(); ++iter)
    {
        cout << *iter << " ";
    }
   
    return 0;
}
```

### Example - Extract Key value from Container

```c++
std::vector<DataId> EventSample::keys() {
  std::vector<DataId> returnValue{};
  std::transform(data.begin(), data.end(), std::back_inserter(returnValue), [](auto& kv) { return kv.first; });
  return returnValue;
}
```