---
title: "[c++] c++14 lambda function"
categories:
  - C++
tags:
  - C++
---

## Why using lambda function
[Iterating Containers](https://developer.internal.ericsson.com/docs/traffic-control/guidelines-and-rules/cpp/style-guide/additions/standard-library/) 
    - for-loop보다 algorithm을 사용하라고 권장

## Compare with for loop
- find_if 와 lamdba 와 일반 for loop 구문을 구분해서 이해하자면, 
    - for loop 구문은 loop 을 순회하는 logic 과 찾고자 하는 logic 이 뒤섞여 있는 방식
    - find_if 와 lamdba 의 조합 : 순회하는 logic 과 찾고자 하는 logic 이 분리되어 있는 방식
- 어떤 기능을 구현할 때 최대한 coupling 없이 구분되도록 coding 하는 것을 추천 
- 그래서, find_if 와 lamdba 함수를 권고
- 속도 측면에서도 lamdba 는 inline 치환이 가능하므로 전혀 문제가 없습니다. 다만, 가독성을 방해하는 무분별한 lamdba 의 사용은 주의가 필요하겠습니다.
