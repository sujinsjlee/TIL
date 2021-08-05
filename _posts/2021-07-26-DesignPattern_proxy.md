---
title: "Design Pattern - Proxy Pattern"
categories:
  - Design Pattern
tags:
  - Design Pattern
---

## Proxy Pattern
> 어떤 객체에 대한 접근을 제어하기 위한 용도로 **대리인이나 대변인에 해당하는 객체를 제공**하는 패턴  
> Proxy Pattern : 프로세스간 통신 (Inter-Process Communication, IPC) 기반의 **Client-Server** 프로그램 모델


- Server

```c++
#include <iostream>
#include "ecourse_dp.hpp"
#include "ICalc.h"
using namespace std;
using namespace ecourse;

class Calc : public ICalc
{
public:
	int Add(int a, int b) { return a + b; }
	int Sub(int a, int b) { return a - b; }
};
Calc calc;


int dispatch( int code, int x, int y )
{
	printf("[DEBUG] %d, %d, %d\n", code, x, y );

	switch( code )
	{
	case 1: return calc.Add( x, y);
	case 2: return calc.Sub( x, y);
	}
	return -1;
}

int main()
{
	ec_start_server("CalcService", dispatch);
}
```

- Client

```c++
#include <iostream>
#include "ecourse_dp.hpp"
#include "ICalc.h"
using namespace std;
using namespace ecourse;

class Calc : public ICalc
{
    int server;
public:
    Calc() { server = ec_find_server("CalcService");    }

    int Add(int a, int b) { return ec_send_server(server, 1, a, b);}
    int Sub(int a, int b) { return ec_send_server(server, 2, a, b);}
};

int main()
{
    Calc* pCalc = new Calc;

	cout << pCalc->Add(1, 2) << endl;
    cout << pCalc->Sub(10, 8) << endl;
}

```

- ICalc

```c++
// ICalc.h

// 참조계수를 책임지는 함수는 인터페이스에 있어야 한다.

struct IRefCount            // IUnknown
{
    virtual void AddRef() = 0;
    virtual void Release() = 0;
    virtual ~IRefCount()  {}
};

struct ICalc : public IRefCount
{
    virtual int Add(int a, int b) = 0;
    virtual int Sub(int a, int b) = 0;

    virtual ~ICalc() {}
};
```



- **Proxy 장점**
  - 명령코드대신 함수호출 사용
  - 보안의 기능을 추가하거나, 자주사용되는 요청에 대한 캐쉬를 추가할 수 도 있다.

- **Proxy <-> Stub**
  - Proxy는 함수 호출을 명령 코드로 변경해서 서버에 전달
  - Stub은 명령코드를 다시 함수 호출로 변경
  - Proxy는 Stub과 통신한다.

- **RPC (Remote Procedure Call)**
  - 다른 프로세스에 있는 함수를 호출하는 개념
  - Java : RMI (Remote Method Inovocation)

- **인터페이스와 참조계수**
  - Proxy Design Pattern 에서는 인터페이스와 reference count를 구현
    - reference count를 책임지는 함수는 인터페이스에 있어야함
    - *EX) ~~~API (interface)*
    - *EX) ~~~Connection Context (Handle reference count)*
  - 참조계수 : reference count
    - 여러 객체가 *하나의 자원*을 공유
    - 단, 몇 개의 객체자 자원을 사용하는지 개수를 관리


- **참고** <!--coding in the office-->
  - Proxy pattern is used for protect resource or control accessibility
  - Sever will receive the following signal from Server
    - Connection Request 
    - Subscribe Request
  - Client will receive the following signal from Server
    - Connection Cfm
    - Connection Rej
    - Subscribe Cfm
    - Subscribe Rej