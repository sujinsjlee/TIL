---
title: "C++ - 상속"
categories:
  - C++
tags:
  - C++
---

## C++ Class Inheritance

- LocalDataBaseImpl

```c++
// FeatureHandlerBase.h
class FeatureHandlerBase
{
public:
  virtual void setFeatureGenericResponsible(FeatureGenericResponsible* featureResponsible) = 0;
}

//TackHandler.h
class TaskHandler: public FeatureHandlerBase
{
    // Parent Class : FeatureHandlerBase
    // Child Class : TaskHandler
  void setFeatureGenericResponsible(FeatureGenericResponsible* featureResponsible) override;
}

// TaskHandler.cc
void TaskHandler::setFeatureGenericResponsible(FeatureGenericResponsible* featureResponsible)
{
  m_featureResponsible = featureResponsible; // featureResponsible will be set as TaskHandler
  m_LocalDataData = m_featureResponsible->getData();
}

// LocalDataBaseImpl.h
class LocalDataBaseImpl: public LocalData,
                         public FeatureGenericResponsible,
{
    // Parent Class : LocalData, FeatureGenericResponsible
    // Child Class : LocalDataBaseImpl
}

// LocalDataBaseImpl.cc
void LocalDataBaseImpl::initFeatureHandler(void)
{
  FeatureHandlerBase* taskHandler = new TaskHandler(); // create TaskHandler object
  taskHandler->setFeatureGenericResponsible(static_cast<FeatureGenericResponsible*>(this)); // this : TaskHandler object
  m_featureHandlerMap.insert(std::pair<FeatureTypeE, FeatureHandlerBase*>(FEAT_TYPE_AAA, taskHandler));
}
```

## virtual function
<!-- C++에서 가상 함수(virtual function)는 파생 클래스에서 재정의할 것으로 기대하는 멤버 함수를 의미합니다.-->
- **A virtual function** allows derived classes to replace the implementation provided by the base class. 

## static_case<type>(obj)

> **Change Object type**


## this
- The **this** pointer holds the address of current object