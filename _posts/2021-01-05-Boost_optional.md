---
title: "Boost::Optional"
categories:
  - Boost
tags:
  - Boost
links: https://mg729.github.io/boost/2021/01/05/Boost_optional/
---
# boost::optional
- Class template **optional** is a wrapper for representing 'optional' (or 'nullable') objects who may not (yet) contain a valid value. 
- Introduced and supported from C++17 in *std::optional* *(defined in header `<optional>`)*  
- Supported in code by including `#include <boost/optional.hpp>`
> It is recommended to use optional<T> in situations where there is exactly one, clear (to all parties) reason for having no value of type T, and where the lack of value is as natural as having any regular value of T.




- Empty return data value

```c++
#include<iostream>
#include<fstream>

std::string ReadFileAsString(const std::string& filepath) {
    std::ifstream stream(filepath);
    if(stream) {
        std::string res;
        //read file
        stream.close();
        return res;
    }
    return std::string(); // return ""; --> empty string
}
int main() {
    std::string data = ReadFileAsString("data.txt");
    if(data != "") // 
    {

    }
}
```

- Utilize optional to deal with no value data

```c++
#include<iostream>
#include<fstream>
#include<optional> //introduced in c++17

std::optional<std::string> ReadFileAsString(const std::string& filepath) {
    std::ifstream stream(filepath);
    if(stream) {
        std::string res;
        //read file
        stream.close();
        return res;
    }
    return {}; // return ""; --> empty string
}
int main() {
    std::optional<std::string> data = ReadFileAsString("data.txt");

    std::string value = data.value_or("Not present");
    if(data.has_value()) //if(data) --> is okay
    {
        //optional has been set
        cout << data.value();
    }
    else 
    {
        //optional has not been set
    }
}
```
- **value_or**
    - if the data is present, it will return to us the value
    - if the data is not set, it will return whatever value parsed in `HERE`.
        - value_or("HERE");
        - usually default value is set in `HERE`



## boost::make_optionl

```c++
optional<T (not a ref)> make_optional( T const& v )
optional<T (not a ref)> make_optional( bool condition, T const& v )
```
- Returns: optional<T>(v) for the deduced type T of v.
- Returns: optional<T>(condition,v) for the deduced type T of v.

## boost::none

```c++
namespace boost {
class none_t {/* see below */};
const none_t none (/* see below */);
} // namespace boost
```
optional<T> supports uninitialized states with a convenient syntax via a constant of the implementation-defined type `boost::none_t`, identified as boost::none.

Starting with Boost version 1.34.0, both `boost::none_t` and `boost::none` are included in `boost/none.hpp`, which is automatically included by `boost/optional/optional.hpp`

This contant is similar in purpose to NULL, except that is not a `null pointer value`. You can use it to initialize an optional<T> instance, which has the same effect of a default constructor, and you can assign it which has the effect of reseting the optional<T> instance. You can also use it in relational operators to make the predicate expression more clear.



## Reference Links
- [cpp reference - optional](https://en.cppreference.com/w/cpp/utility/optional)
- [When to use Optional](https://www.boost.org/doc/libs/1_64_0/libs/optional/doc/html/boost_optional/tutorial/when_to_use_optional.html)
- [How to Deal with OPTIONAL Data in C++](https://www.youtube.com/watch?v=UAAiwObNhQ0)
- [boost/optional/optional.hpp](https://www.boost.org/doc/libs/1_34_0/libs/optional/doc/optional.html#:~:text=The%20expression%20boost%3A%3Anone,be%20used%20as%20the%20parameter.)
- [Boost.optional](https://www.boost.org/doc/libs/1_64_0/libs/optional/doc/html/index.html)
- [boost/none.hpp](https://www.boost.org/doc/libs/1_64_0/libs/optional/doc/html/optional/reference.html#boost_optional.reference.header__boost_none_hpp_)
- [Chapter 21. Boost.Optional](https://theboostcpplibraries.com/boost.optional)
- [Chapter 24. Boost.Variant](https://theboostcpplibraries.com/boost.variant)