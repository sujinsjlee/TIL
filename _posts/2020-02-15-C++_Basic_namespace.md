---
title: "C++ [Basic] namespace"
categories:
  - C++
tags:
  - C++
---

## namespace의 필요성  
* 함수의 구조체등의 **이름 충돌** 해결  

```cpp
#include <stdio.h>

namespace Audio
{
    void init()
    {
        printf("Audio init\n");
    }
}
namespace Video
{
    void init()
    {
        printf("Video init\n");
    }    
}
// global namespace 
void init()
{
    printf("System init\n");
}

int main()
{
    init();
    Audio::init();
    Video::init();
}

```

## namespace 에 있는 요소에 접근하는 3가지 방법  

### qualified name 사용  
> **Audio::init();**  
> qualified name 사용법을 가장 권장  

### using declaration (using 선언)을 사용한 접근  
> **using Audio::init();**  
> init 함수는 Audio 이름 없이 사용 가능  

### using directive (using 지시어)를 사용한 접근  
> **using namespace Audio;**  
> Audio namespace의 모든 요소를 Audio이름 없이 사용가능  

```c++
  
#include <stdio.h>

namespace Audio
{
    void init()  { printf("Audio init\n"); }
    void reset() { printf("Audio reset\n");}
}
using namespace Audio; // using directive

void init()  { printf("global init\n"); }

int main()
{
    Audio::init();
    
    //using Audio::init; // using declaration
    //init();
    //reset(); // error
    
    //using namespace Audio; // using directive
    ::init(); 
    reset();
}
```

`::init()` : global namespace 에 접근하려면 **::**를 사용  


## std namespace  
> C++ 표준의 모든 요소는 **std** namespace 안에 있음  
 
## namespace rule
> Two classes with the same name can be created inside 2 different namespaces in a single program.  
> **Inside a namespace, no two classes can have the same name.**
