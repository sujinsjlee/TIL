---
title: "Tensorflow - Python (5) 데이터를 위한 팁 1"
categories:
  - Tensorflow
tags:
  - Tensorflow
---

## 데이터 타입 조정
- *pandas* 제공함수 활용
- 변수(칼럽) 타입 확인 : **데이터.dtypes**
- 변수를 범주형으로 변경: 
  - **데이터['칼럼명'].astype('category')**
- 변수를 수치형으로 변경 : 
  - **데이터['칼럼명'].astype('int')**
  - **데이터['칼럼명'].astype('float')**
- NA 값 처리
  - NA 갯수체크 : **데이터.isna().sum()**
  - NA 값 채우기 : **데이터['칼럼명'].fillna(특정숫자)**


## 실습 
```python
###########################
# 라이브러리 사용
import pandas as pd
 
###########################
# 파일 읽어오기
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/iris2.csv'
아이리스 = pd.read_csv(파일경로)
아이리스.head()
 
###########################
# 칼럼의 데이터 타입 체크
print(아이리스.dtypes)
 
# 원핫인코딩 되지 않는 현상 확인
인코딩 = pd.get_dummies(아이리스)
인코딩.head()
 
###########################
# 품종 타입을 범주형으로 바꾸어 준다. 
아이리스['품종'] = 아이리스['품종'].astype('category')
print(아이리스.dtypes)
 
# 카테고리 타입의 변수만 원핫인코딩
인코딩 = pd.get_dummies(아이리스)
인코딩.head()
 
###########################
# NA값을 체크해 봅시다. 
아이리스.isna().sum() # comlumn별로 na값이 있는지 체크
아이리스.tail() # tail() : 마지막 5개 행 print
 
###########################
# NA값에 꽃잎폭 평균값을 넣어주는 방법
mean = 아이리스['꽃잎폭'].mean() # mean() : 평균값계산
print(mean)
아이리스['꽃잎폭'] = 아이리스['꽃잎폭'].fillna(mean)
아이리스.tail()
```


> 강의 출처 : [생활코딩](https://opentutorials.org/course/4570)