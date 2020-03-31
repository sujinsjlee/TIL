---
title: "Data Structure - (3) 큐"
categories:
  - Data Structure
tags:
  - Data Structure
link: https://mg729.github.io/datastructure/2020/01/12/DataStructure_(3)_Queue/
---

##  Queue (큐의 구조)
>**First In First Out(FIFO)**

가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조  
스택과 꺼내는 순서가 반대
<ul>
 <li> Enqueue : 큐에 데이터를 넣는 기능 </li>
 <li> Dequeue : 큐에 데이터를 빼는 기능 </li>
</ul>

##  queue - C++ STL Container  
[c++ queue](https://en.cppreference.com/w/cpp/container/queue).  
{% highlight c++ %}
#include <iostream>
#include <queue>
using namespace std;

int main()
{
    queue<int> q1;

    q1.push(10); // push는 push_back 호출.
    q1.push(20);
    q1.push(30);
    
    cout << q1.front() <<endl; //10
    cout << q1.back() <<endl;  //30 
    
    q1.pop();
	
    cout << q1.front() <<endl; //20  
    
}
{% endhighlight %}


```cpp
#include <iostream>
#include <queue>

using namespace std;

int main()
{
	queue<int> q;
	q.push(1);
	q.push(2);
	q.push(3);
	
	q.pop();
	q.push(4);
	q.pop();
			
	while(!q.empty())
	{
		cout << q.front()<< " ";
		q.pop();
	}
	//3 4
	return 0;
}
```

##  Priority Queue  
[c++ priority queue](https://en.cppreference.com/w/cpp/container/priority_queue).  
* 각각의 데이터를 넣을 때마다 데이터의 우선순위번호를 함께넣음  
* 데이터를 넣을때 매겨져있던 우선순위에따라 데이터를 추출하는 순서가 달라지는 구조  
{% highlight c++ %}
#include <iostream>
#include <queue>
using namespace std;


int main()
{
    priority_queue<int> pq;

    pq.push(10);      
    pq.push(20);
    pq.push(15);
    pq.push(12);

    cout << pq.top() << endl; // 20    
    pq.pop();
    cout << pq.top() << endl; // 15   
}
{% endhighlight %}

##  큐의 활용  
* 운영체제에서 멀티태스킹을 위해서 큐가 활용  
* 서로 다른 속도로 실행되는 두 프로세스 스케쥴링 간의 상호작용을 조화시키는 버퍼 역할