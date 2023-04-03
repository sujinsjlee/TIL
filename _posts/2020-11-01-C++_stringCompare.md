---
title: "C++ - String 비교"
categories:
  - C++
tags:
  - C++
link: https://sujinsjlee.github.io/c++/2020/11/01/C++_CompareTwoStrings/
---
# compare two strings in C++

## compare()
```cpp
int main() 
{ 
    string s1("StringA"); 
    string s2("StringBC"); 
    int x = s1.compare(s2); 
  
    if (x != 0) 
        cout << s1 << " is not equal to " << s2 << endl; 
    else if(x == 0)
        cout << s1 << " is equal to " << s2 << endl; 

    if (x > 0) 
        cout << s1 << " is greater than " << s2 << endl; 
    else
        cout << s2 << " is greater than " << s1 << endl;


    return 0; 
} 
```

## operator ==
```cpp
int main() 
{ 
    string s1("StringA"); 
    string s2("StringBC"); 
  
    if (s1 != s2) 
        cout << s1 << " is not equal to " << s2 << endl; 
    else if(s1 == s2)
        cout << s1 << " is equal to " << s2 << endl; 
    return 0; 
} 
```

## Differences between compare() and operator==
```cpp
  // operator ==
  /**
   *  @brief  Test equivalence of two strings.
   *  @param __lhs  First string.
   *  @param __rhs  Second string.
   *  @return  True if @a __lhs.compare(@a __rhs) == 0.  False otherwise.
   */
  template<typename _CharT, typename _Traits, typename _Alloc>
    inline bool
    operator==(const basic_string<_CharT, _Traits, _Alloc>& __lhs,
	       const basic_string<_CharT, _Traits, _Alloc>& __rhs)
    { return __lhs.compare(__rhs) == 0; }
```

* `string::operator==()` is using `string::compare()`
