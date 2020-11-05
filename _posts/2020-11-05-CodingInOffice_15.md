---
title: "[ETC] - Fix Double indirection"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

## Double indirection
```cpp
struct StructTransaction {
  StructTransaction(std::shared_ptr<Transaction> trans)
   : sTrans(trans) {}
  std::shared_ptr<Transaction> sTrans;
};

std::unique_ptr<StructTransaction> sData;

sData->sTrans->handleMessage();
```

* Double indirection above 


## Fix Double indirection
```cpp
std::shared_ptr<Transaction> sTrans;

sTrans->handleMessage();
```

* Fix Double indirection