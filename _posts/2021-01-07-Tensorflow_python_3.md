---
title: "Tensorflow - Python (3) 분류 - 원핫인코딩/softmax"
categories:
  - Tensorflow
tags:
  - Tensorflow
---

## 분류
- 종속변수가 양적데이터(숫자) : 회귀  regression
- 종속변수가 범주형 데이터(이름) : **분류 classification**

## 원핫인코딩 onehot-encoding
- 원핫인코딩 
    - 범주형 데이터를 0 또는 1로 바꾸어주는 과정

## softmax
- Softmax(소프트맥스)
    - 입력받은 값을 출력으로 0~1사이의 값으로 모두 정규화하며 출력 값들의 총합은 항상 1이 되는 특성을 가진 함수
    - Softmax의 출력값은 0~1범위의 확률값이며 모든 확률의 합이 1입니다.
    - y값(종속변수)의 최소값은 0 최대값은 1

> 숙제  
> 분류를 확률 0% ~ 100%로 표현하는 방법 (Sigmoid, Softmax)  


## categorical_crossentropy
- 분류에 사용하는 loss
- "분류"는 모델 compile시 **accuracy** 정보도 같이 확인할 수 있음

## 아이리스 품종 분류 (실습)

```python
###########################
# 라이브러리 사용
import tensorflow as tf
import pandas as pd
 
###########################
# 1.과거의 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/iris.csv'
아이리스 = pd.read_csv(파일경로)
아이리스.head()
 
# 원핫인코딩
아이리스 = pd.get_dummies(아이리스)
아이리스.head()  # 오! 신기해

print(아이리스.columns)

# 종속변수, 독립변수
독립 = 아이리스[['꽃잎길이', '꽃잎폭', '꽃받침길이', '꽃받침폭']]
종속 = 아이리스[['품종_setosa', '품종_versicolor', '품종_virginica']]
print(독립.shape, 종속.shape)
 
###########################
# 2. 모델의 구조를 만듭니다
X = tf.keras.layers.Input(shape=[4])
Y = tf.keras.layers.Dense(3, activation='softmax')(X) # 분류문제는 activation function을 softmax로ㅗ 설정
model = tf.keras.models.Model(X, Y)
model.compile(loss='categorical_crossentropy',
              metrics='accuracy')
 
###########################
# 3.데이터로 모델을 학습(FIT)합니다.
model.fit(독립, 종속, epochs=1000, verbose=0)
model.fit(독립, 종속, epochs=10)
 
###########################
# 4. 모델을 이용합니다
# 맨 처음 데이터 5개
print(model.predict(독립[:5])) 
print(종속[:5])
 
# 맨 마지막 데이터 5개
print(model.predict(독립[-5:]))
print(종속[-5:])
 
###########################
# weights & bias 출력
print(model.get_weights())
```


> 강의 출처 : [생활코딩](https://opentutorials.org/course/4570)