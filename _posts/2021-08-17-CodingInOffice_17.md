---
title: "C++ [STL] update whole existing vector data with new input"
categories:
  - C++
tags:
  - C++
---

## STL - vector 
- `clear()` : [Erases all elements from the container. After this call, size() returns zero.Leaves the capacity() of the vector unchanged.](https://en.cppreference.com/w/cpp/container/vector/clear)
- `shrink_to_fit()` : [Requests the removal of unused capacity.](https://en.cppreference.com/w/cpp/container/vector/shrink_to_fit)


1. myCode
```c++
const std::vector<StudentS>& LocalDataImpl::getPeopleInformation(const std::vector<StudentS>& inputStudents )
{
    m_people.clear();
    m_people.shrink_to_fit(); // std::vector<StudentS> m_people 
 
    StudentS student;
    for (const auto& iStudent : inputStudents)
    {
        student.age = dotData.age;
        student.phone = dotData.phone;
        student.address = dotData.address;
        student.height = dotData.height;
        student.weight = dotData.weight;
        
        m_people.push_back(student);
    }
  
  return m_people;
}
```

2. comment
> if input value and member data has same type, please just assign data with **"="** directly

```c++
typedef struct StudentS
{
    int age;
    int phone;
    string address;
    int height;
    int weight;
    StudentS operator=(const StudentS& data)  
    {
        this->aflag = data.age...;
    }
    bool operator==(const StudentS& data) const 
    {
        return data.aflag == this->aflag && data.bflag == this->bflag;
    }
}StudentS;

const std::vector<StudentS>& LocalDataImpl::getPeopleInformation(const std::vector<StudentS>& inputStudents )
{
    m_people.clear();
    m_people.shrink_to_fit(); // std::vector<StudentS> m_people 
    m_people = inputStudents;
  
    return m_people;
}
```
