---
title: "[c++] STL Map operator=="
categories:
  - C++
tags:
  - C++
---


```c++
#include <iostream>
#include <map>
 
int main()
{
    std::map<int, char> alice{{1, 'a'}, {2, 'b'}, {3, 'c'}};
    std::map<int, char> bob{{7, 'Z'}, {8, 'Y'}, {9, 'X'}, {10, 'W'}};
    std::map<int, char> eve1{{1, 'a'}, {2, 'b'}, {3, 'c'}};
    std::map<int, char> eve2{{2, 'b'}, {1, 'a'}, {3, 'c'}};
 
    std::cout << std::boolalpha;
 
    // Compare non equal containers
    std::cout << "alice == bob returns " << (alice == bob) << '\n';
    std::cout << "alice != bob returns " << (alice != bob) << '\n';
 
    std::cout << '\n';
 
    // Compare equal containers
    std::cout << "alice == eve1 returns " << (alice == eve1) << '\n';
    std::cout << "alice == eve2 returns " << (alice == eve2) << '\n';
    std::cout << "alice != eve1 returns " << (alice != eve1) << '\n';
    std::cout << "alice != eve2 returns " << (alice != eve2) << '\n';
}
```

```
alice == bob returns false
alice != bob returns true

alice == eve1 returns true
alice == eve2 returns true
alice != eve1 returns false
alice != eve2 returns false
```

