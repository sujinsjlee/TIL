---
title: "[ETC] - Code Comment on constructor handling"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
public: false
---

## Code Comment on constructor handling
> 멤버변수 default value 를 특별히 세팅해야하는 경우에, constructor 에서 default value를 세팅하고 추가적으로 바꿀 필요가 있다면, 생성자에서 생성자 멤버 초기화 리스트 (Constructor member initializer list)를 통해서 초기화된 멤버변수를 생성자 내부에서 변경  
> **생성자 내부에서 멤버변수를 추가적으로 초기화 again**  
> 그리고 생성자 초기화 함수용 **init()함수 static으로 구현**하는 것도 고려  
 

For Service in BIT, here is another approach to set Service::m_sysConsts before actual subscription.

Add init(std::map<int16_t, int16_t>) method in Service to update m_sysConsts with input parameter.
Add new attribute(for example, std::map<int16_t, int16_t> m_initSysConsts) in TestContext for system constants to be added in Service::m_sysConsts.
Change codes for SysConst Service start in TestBase::SetUp( )
- Before
  - bit::Service::get()->start(m_sutProc);
- After
  - bit::Service::get()->init(m_testContext.m_initSysConsts);
  - bit::Service::get()->start(m_sutProc);

Change codes for BitNewTest::SetUp()
- Call BitTestBase::SetUp() after setting m_testContext.m_initSysConsts with expecting value.

In my view, it seems to be more general approach for our purpose. Please consider it.