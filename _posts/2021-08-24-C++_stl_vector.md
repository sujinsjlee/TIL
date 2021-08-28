---
title: "[STL Vector] push_back vs. emplace_back"
categories:
  - C++
tags:
  - C++
---

## push_back

> **push_back**은 인자로 필요한 객체를 생성 후  *push_back* 함수 내부에서 다시 한번 복사가 일어난 뒤 *push_back*이 끝날 때 인자들과 객체가 파괴된다. 즉 객체를 하나 추가할 때 쓸데없이 2번 복사하고 파괴한다.

<!-- > **push_back** creates an object required as an argument, then copies are made inside the *push_back* function once again, and when *push_back* ends, the arguments and object are destroyed. That is, when an object is added, it is copied and destroyed twice unnecessarily.-->


<!--참조 링크 : https://m.blog.naver.com/sorkelf/220825930008 -->

## emplace_back

> **emplace_back**은 *push_back*과 같이 vector의 요소 끝에 원소를 추가하는 함수이다. 두 함수의 가장 큰 차이점은, *push_back*은 삽입할 객체를 받아 임시 객체를 만들고 *push_back* 내부에서 복사가 일어난 뒤 vector vector에 추가를 한다. *emplace_back*은 삽입할 객체의 생성자를 위한 인자들을 받아 std::vector 내에서 직접 객체를 생성하여 삽입하므로 임시 객체의 생성과 파괴, 복사(혹은 move)를 하지 않아도 되어 성능상 유리하다는 것이다. 즉 *emplace_back*은 객체를 추가할 때 std::vector 내에서 직접 객체를 추가하고, *push_back*은 임시 객체를 생성 후 *push_back* 함수 내부에서 객체 추가를 위해 복사를 한 뒤 객체 추가를 한다.

<!-- > **emplace_back** is a function that adds an element to the end of an element in a vector like *push_back*. The biggest difference between the two functions is that *push_back* receives the object to be inserted, creates a temporary object, and after copying occurs inside *push_back*, it is added to the vector vector. Since *emplace_back* receives arguments for the constructor of the object to be inserted and directly creates and inserts an object in std::vector, it is advantageous in terms of performance as it does not need to create, destroy, or copy (or move) a temporary object. That is, when adding an object, *emplace_back* adds an object directly in std::vector, and *push_back* creates a temporary object, copies it inside the *push_back* function to add an object, and then adds the object.-->

<!--참조 링크: https://shaeod.tistory.com/630 -->