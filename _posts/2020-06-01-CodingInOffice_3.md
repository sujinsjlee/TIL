---
title: "[ETC] - Using reference value when function call"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---
<!--코딩잘하고싶다-->
## call-by-reference
[call-by-reference 개념](https://wayhome25.github.io/cs/2017/04/11/cs-13/)

## 함수호출할 때 return value로 쓰이는 값이라면 local변수 만들어서 복사비용 증가시키지말고 reference value를 사용

```cpp
vector<string> getInterfaceList(vector<string>* ifList) {
  vector<string> interfaceList; //It will be more efficient to define this as input argument.

  for (int i{0}; ((size_t)i) < ifList->size(); i++) {
	///
  }

  return interfaceList;
}

vector<string> getLocalAttributes(const vector<string>& Nvs) {
  vector<string> localNvs;  //It will be more efficient to define this as input argument.

  for (auto attr : Nvs) {
    std::string attrName = attr->getName();
    if (attrName == "interfaceList") {
      auto interfaceList = getInterfaceList(attr->getValue());
    }
  }
  return localNvs;
}
```

- 불필요한 복사하지 말고 reference형태로 변수 바꾸도록


```cpp

vector<string> getInterfaceList(vector<string>* ifList, vector<string>& interfaceList) {
  for (int i{0}; ((size_t)i) < ifList->size(); i++) {
	///
  }

  return interfaceList;
}

vector<string> getLocalAttributes(const vector<string>& Nvs, vector<string>& localNvs) {
  for (auto attr : Nvs) {
    std::string attrName = attr->getName();
    if (attrName == "interfaceList") {
      auto interfaceList = getInterfaceList(attr->getValue());
    }
  }
  return localNvs;
}
```