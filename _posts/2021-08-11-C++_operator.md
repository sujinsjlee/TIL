---
title: "[Comment] struct operator overloading"
categories:
  - C++
tags:
  - C++
---

## overloading
[overloading assignments c++](https://www.ibm.com/docs/en/i/7.1?topic=only-overloading-assignments-c)

```c++
typedef struct DataS
{
    bool aflag = false;
    bool bflag = false;
    Data& operator=(const Data& data)
    {
      this->aflag = data.aflag;
      this->bflag = data.bflag;
      return *this;
    }
    bool operator==(const DataS& data) const 
    {
        return data.aflag == this->aflag && data.bflag == this->bflag;
    }
} DataS;
```



