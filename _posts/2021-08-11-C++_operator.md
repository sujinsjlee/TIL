---
title: "[Comment] struct operator overloading"
categories:
  - C++
tags:
  - C++
---

## STL - vector 
- emplace_back(....)

```c++
typedef struct DataS
{
    bool aflag = false;
    bool bflag = false;
    bool operator==(const DataS& data) const 
    {
        return data.aflag == this->aflag && data.bflag == this->bflag;
    }
} DataS;
```



