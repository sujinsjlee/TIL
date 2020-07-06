---
title: "코딩잘하고싶다 - C++ Concept"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

## Concept 
- __Client__ : The originator of a request. The destinaction endpoint of a response.  
- __Server__ : The destination endpoint of a request. The originator of a response.  
- __Observer__ : A client that can register itself using a modified GET message. The observer is then connected to a resource, and if the state of that resource changes, the server will send a notification back to the observer.  
- __Provider__ : The provider is a server that processes the requests issued by clients.  
- __User__  
- __call__ __back__   
- __Endpoint__  


## Application Framework
- 프로세스 실행순서  
1. 전역변수 생성자. 기반 클래스 생성자
2. main 함수 실행

## Observer Pattern
- 객체 사이의 1:N 의 종속성을 정의하고 한 객체의 상태가 변하면 종속된 다른 객체에 통보가 가고 자동으로 수정이 일어나게 한다.  
- Obeserver 의 대상 : Subject  


## 상속
```c++

class Person
{
    std::string name;
    int age;
};

class Professor : public Person
{
    int major;    
};

class Student : public Person
{
    int id;
};

class ParttimeStudent : public Student
{
    int salary;
};

int main()
{
    Professor p;
    Student   s;
}

```

- Student와 Professor를 만들때 Person으로부터 상속을 받는다.  
- 한 클래스가 다른 클래스에서 정의된 속성들을 이어받아서 사용하는 것  
- S/W의 재사용성 지원  
- __다형성__을 활용한 객체지향 디자인 기법  
- UML 표기법 :  Student -> Person 

## protected 
```cpp
class Base
{
private:   int a;
protected: int b;
public:    int c;
};

class Derived : public Base
{
public:
    void foo()
    {
        a = 10; // error
        b = 10; // ok -- 파생클래스에서는 접근가능
        c = 10; // ok 
    }
};

int main()
{
    Derived derv;
    derv.a = 10; // error
    derv.b = 10; // error -- 외부에서는 접근 불가능
    derv.c = 10; // ok
}

```

## 상속에서의 생성자/소멸자 호출 순서
- 파생클래스의 생성자에서 기반 클래스의 생성자를 호출하는 코드를 컴파일러가 생성해주는 것

## Upcasting
```cpp
class Shape
{
public:
    int color;
};

class Rect : public Shape
{
public:
    int x, y, w, h;
};

int main()
{
    Rect rect;
    
    Rect*  p1 = &rect; // ok
    int*   p2 = &rect; // error. 
    Shape* p3 = &rect; // ok  
    
    Shape& r = rect;   // ok. 
    
}
```
- 기반 클래스 타입의 포인터로 파생클래스를 가리킬 수 있다  
- 기반 클래스 타입의 참조로 파생클래스를 가리킬 수 있다   

```cpp
class Shape
{
public:
    int color;
};
class Rect : public Shape
{
public:
    int x, y, w, h;
};

int main()
{
    Rect rect;

    Shape* p = &rect; 
    
    p->color = 0; // ok
    p->x = 0;     // error
    static_cast<Rect*>(p)->x = 0; // ok
    
}
```
- 기반 클래스 타입의 포인터로 파생클래스를 가리킬 때
	- 기반 클래스의 멤버는 접근할 수 있지만  
	- **파생클래스가 추가한 멤버는 접근할 수 없다**  
	- 파생클래스가 추가한 멤버에 접근하려면 **포인터를 파생클래스타입으로 캐스팅**해야한다  
	

## 가상함수 오버라이드
```cpp
#include <iostream>

class Shape
{
public:
    void Draw() { std::cout << "Shape::Draw" << std::endl; }
};

class Rect : public Shape
{
public:
    void Draw() { std::cout << "Rect::Draw" << std::endl; }
};

int main()
{
    Shape s; s.Draw(); // Shape::Draw
    Rect r;  r.Draw(); // Rect::Draw
    
    Shape* p = &r;     //
    p->Draw();         // Shape::Draw
}
```

- 함수 오버라이드	  
	- 기반클래스가 가진 함수를 파생클래스가 다시 만드는 것  
	- 기반 클래스 포인터로 파생클래스를 가리킬 때 override된 함수호출하면 C++은 기반 클래스 함수 호출  
	
## 함수 바인딩 (binding)
- p->Draw() 를 어느 함수와 연결할 것인가?
	1. **컴파일할 때 결정** - static binding
	2. **실행할 때 결정** - dynamic binding  
- c++은 기본적으로 컴파일 할 때 함수호출을 결정한다.  

## 가상함수
```cpp
  
#include <iostream>

class Shape
{
public:
    virtual void Draw() { std::cout << "Shape::Draw" << std::endl; }
};
class Rect : public Shape
{
public:
    virtual void Draw() { std::cout << "Rect::Draw" << std::endl; }
};

int main()
{
    Shape s; 
    Rect r;  
    
    Shape* p = &r;
    
    p->Draw();    // Rect::Draw
}
```
- 어느 함수를 호출할지는 컴파일 시간에 하지 말고 **실행할 때 결정**해달라는 것  
- 메모리에 있는 객체를 조사한 후 함수 호출  

## 가상 함수 관련 문법 정리
```cpp
class Base
{
public:
    virtual void f1()    {}
    virtual void f2(int) {}
    virtual void f3() const {}
    virtual void f4() {}
};

class Derived : public Base
{
public:
//    virtual void ff1() override {}
//    virtual void f2(double) override {}
//    virtual void f3() override {}
    
    virtual void f4() final {}
};
class Derived2 : public Derived
{
public:
    virtual void f4()  {}
};

```
- 파생클래스에서 가상함수 재정의할 때 **virtual 은 붙여도되고 안붙여도됨**
	- 되도록이면 붙이는 것이 가독성이 좋다  
- override
	- 실수를 방지하기 위해 **override**를 붙이는 것이 좋다  
- final  
	- 파생클래스에서 **가상함수를 재정의할 수 없도록 하기 위해**  
- 선언과 구현으로 분리할 때는 
	- virtual, override, final 키워드는 선언부에만 표기하고 구현부에는 표기하지 않는다  
	
- 어떤 클래스가 기반클래스로 사용된다면
	- **소멸자를 반드시 가상함수로 만들어야한다**  

## 순수가상함수 (pure virtual funtion)
```cpp
class Shape
{
public:
    virtual void Draw() = 0;
};

class Rect : public Shape
{
public:
    virtual void Draw() { }  
};

int main()
{
    Shape  s; // error
    Shape* p; // ok
    
    Rect r; //r 객체를 사용하기 위해서는 Draw를 구현해야
}
```
- __순수가상함수__  
	- 함수의 구현부가 없고, 선언부가=0으로 끝나는 가상함수  
- __추상클래스__  
	- 순수 가상 함수가 한 개 이상 있는 클래스  
- 추상 클래스 특징 : 객체를 생성할 수 없다(함수 구현이 안되어있으므로)  
	- 포인터 변수는 만들 수 있다(가리키기만 할 것이니까)  
- 추상클래스로부터 파생된 클래스  
	- 기반 클래스의 순수 가상함수의 구현부를 제공하지 않으면 역시 추상클래스다
- 추상클래스의 설계의도  
	- 파생클래스에게 특정 멤버함수를 반드시 만들어야한다고 지시하는 것  
	
	
## 인터페이스
```cpp
#include <iostream>

class Camera
{
public:
    void take() 
    {
         std::cout << "take picture" << std::endl; 
    }
};

class HDCamera
{
public:
    void take() 
    {
         std::cout << "take picture HD" << std::endl; 
    }
};

class People
{
public:    
    void useCamera(Camera* p) { p->take();}
    void useCamera(HDCamera* p) { p->take();}
};

int main()
{
    People p;
    Camera c1;
    p.useCamera(&c1);
    
    HDCamera hd;
    p.useCamera(&hd);
}

```
- **강한 결합**
	- 객체와 다른 개체와의 관계가 강하게 연결되어있는 것  
	- 교체 불가능하고 확장성이 없다  

```cpp
#include <iostream>

// 인터페이스
// 보통 public으로 함수선언하기때문에 인터페이스는 struct로 구현
struct ICamera
{
    virtual void take() = 0;
};


class People
{
public:    
    void useCamera(ICamera* p) { p->take();}
};


class Camera : public ICamera
{
public:
    void take() 
    {
         std::cout << "take picture" << std::endl; 
    }
};


class HDCamera : public ICamera
{
public:
    void take() 
    {
         std::cout << "take picture hd" << std::endl; 
    }
};

int main()
{
    People p;
    Camera c1;
    p.useCamera(&c1);
    
    HDCamera c2;
    p.useCamera(&c2);

}

```	
- 사람과 카메라 제작자 사이에 지켜야하는 **규칙을 먼저 설계**  
- 규칙은 **추상클래스를 사용해서 설계**  
	- 모든 카메라는 ICamera 인터페이스를 구현해야한다  

- 약한 결합
	- 객체와 다른 개체와의 관계가 약하게 연결되어있는 것  
	- 인터페이스를 사용해서 통신  
	- 교체 가능하고 확장성이 좋다  

## RTTI

## 다중 상속 

