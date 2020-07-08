---
title: "코딩잘하고싶다 - C++ 상속"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

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
- Run Time Type Information  
	- 실행시간에 **타입의 정보를 얻을 때 사용**하는 기술  

- `<typeinfo>` 헤더를 포함해야  RTTI 기술을 사용할 수 있음  
- **typeid** 연산자를 사용하면 타입의 정보를 담은 **type_info**객체를 얻을 수 있다  
- type_info 객체의 멤버함수 **name()** 사용  

```cpp
#include <iostream>
#include <typeinfo>

int main()
{
    int  n1 = 10;
    auto n2 = n1; // n2 - int 
    
    const std::type_info& t1 = typeid(n2);
    
    std::cout << t1.name() << std::endl;  //int
}
```
- std::type_info  
	- 타입의 정보를 담고 있는 클래스  
	- 사용자가 직접 객체를 만들수는 없고, **typeid()** 연산자를 통해서만 얻을 수 있음  

- 변수 n 이 int 타입인지 **조사**하는 일반적인 코드
```cpp
if( typeid(n2) == typeid(int))
{
}
```
## dynamic_cast
- 함수가 인자로 기반클래스의 포인터를 받으면  
	- 기반 클래스 뿐 아니라 **모든 파생 클래스를 전달**받을 수 있다  

- **기반 클래스 포인터로 파생 클래스의 고유멤버에 접근할 수 없다**  
	- 파생클래스의 고유멤버에 접근하려면 파생클래스 타입으로 캐스팅(Downcasting) 해야한다  

- typeid
	- 가상함수가 없는 객체 (non plymorphic type): 컴파일 시간에 포인터 타입으로 조사  
	- 가상함수가 있는 객체 (plymorphic type): 실행시간 타입조사  
	
```cpp
#include <iostream>
#include <typeinfo>

class Animal 
{
public:
    virtual ~Animal() {}
};

class Dog : public Animal 
{
public:
    int color;
};

void foo(Animal* p)
{
    //const std::type_info& t = typeid(p);
    const std::type_info& t = typeid(*p);
    std::cout << t.name() << std::endl;
    
    if ( typeid(*p) == typeid(Dog))
    {
        Dog* pDog = static_cast<Dog*>(p);
        pDog->color = 10;
        std::cout << "Dog" << std::endl;
    }
}

int main()
{
    Animal a; foo(&a);
    Dog    d; foo(&d);    
}
```
- upcasting vs. downcasting
	- upcasting : 파생클래스 포인터를 기반 클래스 타입으로 캐스팅하는 것  
		- 항상 안전하다
	- downcasting : 기반 클래스 포인터를 파생 클래스 타입으로 캐스팅하는 것  
		- 안전하지 않을 수도 있다  

- downcasting 과 casting 연산자  
	- **static_cast** : 잘못된 downcasting을 조사할 수 없다  
		- 단, 컴파일 시간에 캐스팅을 수행하므로 오버헤드가 없다  
	- **dynamic_cast** : 잘못된 downcasting을 하면 0을 반환함  
		- 실행 시간에 캐스팅을 수행하므로 약간의 오버헤드가 있다  
		
- 즉 아래 코드에서 Dog 객체가 확실하다면 static_cast를 쓰는게 좋은데 Dog 일지아닐지 불확실하면 dynamic_cast  

```cpp
#include <iostream>
#include <typeinfo>

class Animal 
{
public:
    virtual ~Animal() {}
};

class Dog : public Animal 
{
public:
    int color;
};

void foo(Animal* p)
{
    //Dog* pDog = static_cast<Dog*>(p);
    
    Dog* pDog = dynamic_cast<Dog*>(p);
    
    if ( pDog != 0 )
    {
        pDog->color = 10;
    }
    std::cout << pDog << std::endl;
}

int main()
{
    Animal a; foo(&a);
    Dog    d; foo(&d);    
}
```
## 다중 상속 
- 다중 상속이란? 
	- 클래스가 2개 이상의 기반 클래스로 부터 **상속** 되는 것  
- 다중상속의 문제점  
	- 서로다른 기반클래스에 동일 이름의 멤버가 있을 때 이름 충돌  

	
```cpp
class InputFile
{
public:
    void read() {}
    void open() {}
};

class OutputFile
{
public:
    void write(){}
    void open() {}
};

class IOFile : public InputFile, public OutputFile
{    
};

int main()
{
    IOFile file;
    //file.open();
    file.InputFile::open();
}
```


- 다이아몬드 상속이란?
	- virtual 상속을 사용하면 File의 인스턴스가 메모리에 한번만 형성된다  


```cpp
#include <iostream>
#include <string>

class File 
{
public:
    std::string filename;
    void open() {} // filename À» »ç¿ë
};

class InputFile : virtual public File 
{
public:
    void read() {}
};
class OutputFile : virtual public File
{
public:
    void write(){}
    void open() {}
};
class IOFile : public InputFile, public OutputFile
{    
public:
};

int main()
{
    IOFile file;    
    
    file.open();

        
    
}
```	
