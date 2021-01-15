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

- Example 1
    - when using make_optional - can utilize condition
    - Creates an optional<T> initialized with 'val' IFF cond is true, otherwise creates an **uninitialized optional**.
    
```cpp
#include "boost/optional/optional.hpp" // boost/none.hpp is included automatically

boost::optional<int> foo ( int a )
{
  return some_condition(a) ? boost::make_optional(a) : boost::none ; 
  // NOTE: in real code you can just use this: make_optional(some_condition(a), a) 
}
```

- defined code 

```cpp
typedef optional_detail::optional_base<T> base ;
// Creates an optional<T> initialized with 'val' IFF cond is true, otherwise creates an uninitialzed optional<T>.
// Can throw if T::T(T const&) does
optional_base ( bool cond, argument_type val )
  :
  m_initialized(false)
{
  if ( cond )
    construct(val);
}

// Creates an optional<T> initialized with 'val' IFF cond is true, otherwise creates an uninitialized optional.
// Can throw if T::T(T const&) does
optional ( bool cond, argument_type val ) : base(cond,val) {}


// Returns optional<T>(cond,v)
template<class T>
inline
optional<T> make_optional ( bool cond, T const& v )
{
  return optional<T>(cond,v);
}
```
## uninitialized optional
- **uninitialized optional**
    - In C++ there is no formal notion of uninitialized objects, which means that objects always have an initial value even if indeterminate. As discussed on the previous section, this has a drawback because you need additional information to tell if an object has been effectively initialized. One of the typical ways in which this has been historically dealt with is via a special value: EOF,npos,-1, etc... This is equivalent to adding the special value to the set of possible values of a given type.  
    - when a variable is declared as optional<T> and no initial value is given, the variable is formally uninitialized. A formally uninitialized optional object has conceptually no value at all and this situation can be tested at runtime. It is formally undefined behavior to try to access the value of an uninitialized optional. An uninitialized optional can be assigned a value, in which case its initialization state changes to initialized. Furthermore, given the formal treatment of initialization states in optional objects, it is even possible to reset an optional to uninitialized.

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