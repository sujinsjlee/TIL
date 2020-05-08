---
title: "Data Structure - (6) 해쉬테이블"
categories:
  - Data Structure
tags:
  - Data Structure
link: https://mg729.github.io/datastructure/2020/01/30/DataStructure_(6)_HashTable/
---

## Hash Table 구조  
> **Hash Table**: 키에 대한 데이터를 저장하는 데이터 구조  
> 키만 알면 데이터가 어디에 저장되어있는지 알 수 있는 데이터 구조  

![HashTable](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/1280px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)  
[Hash Table Wiki](https://en.wikipedia.org/wiki/Hash_table)      

* **Key** 를 통해 바로 데이터를 받아올 수 있으므로 속도가 빠름 

## Term   
* <u>해쉬(Hash)</u> : 임의 값을 **고정 길이**로 변환하는 것
* <u>해쉬 테이블 (Hash Table)</u> : **키**와 키와 연관된 **해쉬 값**의 데이터가 저장된 공간  
* <u>해싱 함수 (Hashing Function)</u> : **키를 입력**으로 넣어서 데이터가 저장되어있는 해쉬 테이블의 **해쉬 주소를 리턴**하는 함수  
* <u>해쉬 값 (Hash Value), 해쉬 주소(Hash Address)</u> : Key를 해싱함수로 연산해서 알아낼 수 있는 **리턴값**   
* <u>슬롯 (Slot), 버킷 (Bucket)</u> : **해쉬 값**을 저장하는 공간   

## Hash Table 의 장단점과 주요 용도
1. **장점**  
	* 데이터 저장/읽기 속도가 빠르다 **(검색 속도가 빠르다)**  
		* 검색에서 배열보다 해쉬테이블 구조가 좋은 이유
			* 배열 : index별로 일일이 검색해야, index를 순차적으로 검색할 때 찾고자 하는 데이터가 배열의 마지막 인덱스에 값인 경우 시간이 오래걸림  
			* 해쉬테이블 : 데이터를 받고 그에 해당하는 키를 찾으면 해쉬함수를 한번만 돌리면 바로 그 데이터 저장위치를 해쉬테이블에서 찾을 수 있음  
	* 키에 대한 해쉬 값이 있는지 없는지 중복체크가 쉬움   
		* 배열같은 경우는 index 에 대한 값이 있는지 없는지 중복체크할때 기존 데이터를 일일이 봐야함    		
2. **단점**  
	* 일반적으로 **저장공간**이 많이 필요  
	* 여러 key에 해당하는 해쉬 주소가 동일한 경우 **충돌**이 발생
		* 따라서 충돌을 해결하기 위한 별도의 자료구조가 필요  
3. **주요 용도**    
	* 검색이 많이 필요한 경우  
	* 저장, 삭제, 읽기가 빈번한 경우  
	* 캐쉬 구현시 (중복확인이 쉽기 때문) - 웹 프로그래밍에서 캐쉬 기능을 구현할 때 바뀐 데이터만 서버에서 처리  
	* 블록체인  

## 충돌해결책
![Hash_Table_Collision](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/1280px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)  
[Hash Table wiki_collision resolution](https://en.wikipedia.org/wiki/Hash_table#Collision_resolution)   
해쉬 테이블의 가장 큰 문제는 **충돌(Collision)**  
: 한 개 이상의 key값이 동일한 hash address에 저장이 되어야 되는 경우  

1. **체이닝**
![Chaining](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Hash_table_5_0_1_1_1_1_0_LL.svg/1920px-Hash_table_5_0_1_1_1_1_0_LL.svg.png)  
* Open Hashing 기법 (개방해슁) : 해쉬 테이블 저장 공간 외의 공간을 활용  
	* 충돌이 일어나면 **연결리스트** 자료구조를 활용  
	* 링크드 리스트로 데이터를 추가로 뒤에 연결시켜서 저장하는 방법  	
	* 메모리 추가 문제
2. **선형 조사법**
![LinearProbing](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Hash_table_5_0_1_1_1_1_0_SP.svg/1024px-Hash_table_5_0_1_1_1_1_0_SP.svg.png)  
* Closed Hashing 기법 (폐쇄 해슁) : 해쉬테이블 저장공간 안에서 충돌문제를 해결  
	* 충돌이 일어나면 hash address 의 다음 address 부터 맨 처음나오는 빈공간에 저장  
	* 저장공간 활용도를 높이기 위한 방법  
	* open addressing method
3. **빈번한 충돌을 개선하는 방법**  
* 해쉬 함수의 재정의 및 해쉬 테이블 저장공간 확대  
	* 저장 공간을 두배로 증가시키는 것이 일반적 해결 방법  

## 해쉬 함수
* **std::hash**  
[c++ utility library - std::hash](https://en.cppreference.com/w/cpp/utility/hash)  
[Any bulit in hash function in C++](https://stackoverflow.com/questions/6200483/any-built-in-hash-method-in-c)  
[Key type as string, then why not int type?](https://stackoverflow.com/questions/38304877/why-stdhashint-seems-to-be-identity-function)  
	* Defined in header **functional**  
	* Argument type : Key  
	* Return type : std::size_t  
	* 매개 변수(Key)의 해시 값을 나타내는 std :: size_t 유형의 값을 리턴  
		* **size_t**는 해당 시스템에서 어떤 객체나 값이 포함할 수 있는 최대 크기의 데이터를 표현하는 타입(unsigned 형)  
	* **hash support for strings** (hash 에서 support하는 key는 cppreference **Standard specializations for library types** 항목 참고)  
	
```c++
#include <iostream>
#include <string>
#include <functional>

using namespace std;

int main()
{
    string str = "Sunny";
    size_t str_hash = hash<string>{}(str);
    cout << "hash value is " << str_hash << endl; //1392135701625917544
}
```

* **SHA-256**(<u>Secure Hash Algorithm</u>, 안전한 해시알고리즘)  
[SHA-256](http://www.zedwood.com/article/cpp-sha256-function) 
	* 대표적인 해시 알고리즘  
	* 문자열이 입력되면 고정된 길이의 매우 긴 문자열로 반환해주는 알고리즘  
	* 어떤 데이터에도 유일한 고정된 크기의 고정값을 리턴해주므로, 해쉬함수로 유용하게 활용 가능  
	* __SHA-256__  
		* 가장 많이 사용되는 해시 함수  
		* 해쉬의 결과 : **128 bit**  
		* 비트코인, 블록체인 시스템에서 활용  
* *한국인터넷진흥원 [KISA](https://seed.kisa.or.kr/kisa/Board/21/detailView.do)에서는 256비트 해시함수 SHA-256을 쉽게 활용할 수 있도록, 소스코드를 배포하고 있습니다.*


## 시간복잡도  
> 저장 및 데이터 읽는 데 걸리는 시간 복잡도  
> 일반적인 경우 (Collision이 없는 경우) :  **O(1)**  
> 최악의 경우 (Collision이 모두 발생하는 경우) : **O(n)**  

해쉬 테이블의 경우, 일반적인 경우를 기대하고 만들기 때문에, 시간복잡도는 O(1)이라고 할 수 있음  

### 참고 개념  
* **Open Addressing**
	* Open addressing strategy requires, that **hash function has additional properties.** In addition to performing uniform distribution, it should also **avoid clustering of hash values**, which are consequent in probe's order. 

<!--!!!-->
## C++ Code  
> [해쉬 테이블 - by Linear Probing기법](#hash_table_with_linear_probing)  
> [해쉬테이블 - by Chaining 기법](#hash_table_with_chaining))  
> [Hash Table 구현 by list](#hash_table_by_list)  

*  [C++ Hash Table Implementaion](http://www.algolist.net/Data_structures/Hash_table)  

<!--http://www.algolist.net/Data_structures/Hash_table/Simple_example-->
## hash_table_with_linear_probing  

```cpp
constexpr int TABLE_SIZE = 128; 

class HashBucket
{
private:
	int key;
	int hashValue;
public:
	HashBucket(int key, int hashValue)
	{
		this->key = key;
		this->hashValue = hashValue;
	}
	int getKey()
	{
		return key;
	}
	int getHashValue()
	{
		return hashValue;
	}
};

class HashTable
{
private:
	HashBucket **table;
public:
	HashTable()
	{
		table = new HashBucket*[TABLE_SIZE];
		for(int i = 0; i < TABLE_SIZE ; ++i)
		{
			table[i] = nullptr;
		}
	}
	
	int get (int key)
	{
		int hash = (key % TABLE_SIZE);
		while(table[hash] != nullptr && table[hash]->getKey() != key)
		{
			hash = (hash+1) % TABLE_SIZE;
		}
		if(table[hash] == nullptr)
			return -1;
		else 
			return table[hash]->getHashValue();
	}
	void put (int key, int value)
	{
		int hash = (key % TABLE_SIZE);
		while(table[hash] != nullptr && table[hash]->getKey() != key)
		{
			hash = (hash+1) % TABLE_SIZE;
		}
		if(table[hash] != nullptr)
			delete table[hash];
		else 
			table[hash] = new HashBucket(key, value);
	}
	
	~HashTable()
	{
		for(int i = 0; i < TABLE_SIZE; ++i)
			if(table[i] != nullptr)
				delete table[i];
		
		delete[] table;
		
	}
};
``` 


<!--http://www.algolist.net/Data_structures/Hash_table/Chaining-->
## hash_table_with_chaining  

```cpp
constexpr int TABLE_SIZE = 128; 

class LinkedHashBucket
{
private:
	int key;
	int hashValue;
	LinkedHashBucket * next;
public:
	LinkedHashBucket(int key, int hashValue)
	{
		this->key = key;
		this->hashValue = hashValue;
		this->next = nullptr;
	}
	int getKey()
	{
		return key;
	}
	int getHashValue()
	{
		return hashValue;
	}
	void setHashValue(int value)
	{
		this->hashValue = value;
	}
	LinkedHashBucket *getNext()
	{
		return next;
	}
	void setNext(LinkedHashBucket *next)
	{
		this->next = next;
	}
};

class HashTable
{
private:
	LinkedHashBucket **table;
public:
	HashTable()
	{
		table = new LinkedHashBucket*[TABLE_SIZE];
		for(int i = 0; i < TABLE_SIZE ; ++i)
		{
			table[i] = nullptr;
		}
	}
	
	int get (int key)
	{
		int hash = (key % TABLE_SIZE);
		if(table[hash] == nullptr)
			return -1;
		else 
		{
			LinkedHashBucket * bucket = table[hash];
			while(bucket != nullptr && bucket->getKey() != key)
				bucket = bucket->getNext();
			if(bucket == nullptr)
				return -1;
			else 
				return bucket->getHashValue();
		}
	}
	void put (int key, int value)
	{
		int hash = (key % TABLE_SIZE);
		if(table[hash] == nullptr)
			table[hash] = new LinkedHashBucket(key, value);
		else
		{
			LinkedHashBucket * bucket = table[hash];
			while(bucket -> getNext() != nullptr)
				bucket = bucket->getNext();
			if(bucket->getKey() == key)
				bucket->setHashValue(value);
 			else
 				bucket->setNext(new LinkedHashBucket(key, value));
		}
	}
	void remove(int key)
	{
		int hash = key%TABLE_SIZE;
		if(table[hash] != nullptr)
		{
			LinkedHashBucket *prevBucket = nullptr;
			LinkedHashBucket *bucket = table[hash];
			
			while(bucket->getNext() != nullptr && bucket->getKey() != key)
			{
				prevBucket = bucket;
				bucket = bucket->getNext();
			}
			if(bucket->getKey() == key)
			{
				if(prevBucket == nullptr)
				{
					LinkedHashBucket * nextBucket = bucket->getNext();
					delete bucket;
					table[hash] = nextBucket;
				}
				else
				{
					LinkedHashBucket * nextBucket = bucket->getNext();
					delete bucket;
					prevBucket->setNext(nextBucket);
				}
			}
		}
	}
	
	~HashTable()
	{
		for(int i = 0; i < TABLE_SIZE; ++i)
		{
			if(table[i] != nullptr)
			{
				LinkedHashBucket * prevBucket = nullptr;
				LinkedHashBucket * bucket = table[i];
				while(bucket != nullptr)
				{
					prevBucket = bucket;
					bucket = bucket->getNext();
					delete prevBucket;
				}
			}
			delete[] table;
		}
	}

};
``` 


## hash_table_by_list
[Hash Table implementataion by list - Youtube tutorial](https://www.youtube.com/watch?v=2_3fR-k-LzI&t=35s)  


```cpp
#include<iostream>
#include<list> //해쉬 테이블 구현을 위해 linked list활용
#include<cstring> // string c++ header
				//key will be string type, value will be integer type	 
using namespace std;

//HashTable to implement - phone book

class HashTable
{
private:
	static const int hashGroups = 10; //  10개의 list  
	list<pair<int, string>> hash_table[hashGroups]; //key (int), hash_value (string)
public:
	bool isEmpty() const;
	int hashFunction(int key);
	void insertData(int key, string value);
	void removeData(int key);
	string searchTable(int key);
	void printTable();
};

bool HashTable::isEmpty() const//해쉬테이블이 비어있는지 체크 
{
	// 내가 선언한 table 은 list 객체를 가지고 있는 해쉬테이블배열이다
	// 각각의 list객체는 pair를 가지고 있다. 
	int sum = 0;
	for (int i = 0; i <hashGroups; ++i)
	{
		sum += hash_table[i].size();
	} 
	if(!sum)
	{
		return true;
	}
	return false;
}
int HashTable::hashFunction(int key)
{
	return key % hashGroups;
}

void HashTable::insertData(int key, string value)
{
	int hashValue = hashFunction(key);
	auto& slot = hash_table[hashValue];
	auto iter = begin(slot);
	bool keyExists = false;
	for(; iter != end(slot); ++iter)
	{
		if(iter->first == key)
		{
			keyExists = true;
			iter->second = value;
			cout << "[Warning] : Key exitsts, Value replaced" <<endl;
			break;
		}
	}
	if(!keyExists)
	{
		slot.emplace_back(key, value);
	}
	
	return;
}

void HashTable::removeData(int key)
{
	int hashValue = hashFunction(key);
	auto& slot = hash_table[hashValue];
	auto iter = begin(slot);
	bool keyExists = false;
	for(; iter != end(slot); ++iter)
	{
		if(iter->first == key)
		{
			keyExists = true;
			iter = slot.erase(iter);
			cout << "[Info] : Data removed" <<endl;
			break;
		}
	}
	
	if(!keyExists)
	{
		cout << "[Waning] : Key not found. Pair not removed" <<endl;
	}
}

string HashTable::searchTable(int key)
{
	
}

void HashTable::printTable()
{
	for(int i = 0; i < hashGroups; ++i)
	{
		if(hash_table[i].size() == 0)
		continue;
		
		auto iter = hash_table[i].begin();
		for(; iter != hash_table[i].end(); ++iter)
		{
			cout << "Key : " << iter->first << ", Value : " << iter->second << endl;
		}
	}
	return;
}

int main()
{
	HashTable HT;
	if(HT.isEmpty())
	{
		cout << "Hash Table is Empty" <<endl; 
	}
	
	HT.insertData(905, "Jim");
	HT.insertData(702, "Andy");
	HT.insertData(234, "Kylie");
	HT.insertData(406, "Tom");
	HT.insertData(289, "Sally");
	HT.insertData(289, "Judy");
	
	HT.printTable();
	
	HT.removeData(905);
	HT.printTable();
	
	return 0;
}
``` 
