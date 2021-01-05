---
title: "Tensorflow - Python"
categories:
  - Tensorflow
tags:
  - Tensorflow
---

## Tensorflow
> Tensorflow 라이브러리를 이용하여 딥러닝을 구현하기  

- **TensorFlow : 라이브러리**
    - *TensorFlow* / Pytorch / Caffe2 / theano...
    - 코드 라이브러리

- **DeepLearning : 알고리즘**
    - *Neural Network == Deep Learning*/ Decision Tree / Random Forest / KNN / SVM
    - 이론

- **회귀 분류 : 문제(of 지도학습)**
    - 알고리즘이 해결하는 대표적인 문제

- **Machine Learning** : 지도/비지도학습과 같은 기능을 포괄적으로 머신러닝이라고 함
- **AI** : 머신러닝이 오늘날 인공지능을 구현하는 유망한 분야

## 지도학습
- 지도학습
    - 1. 과거의 데이터를 준비합니다.
    - 2. 모델의 구조를 만듭니다.
    - 3. 데이터로 모델을 학습(**FIT**)합니다.
    - 4. 모델을 이용합니다.

## 환경설정 - Google Colaboratory
> python 언어 테스트 환경  
> **jupyter notebook** /Google Colaboratory (google driver platform에서 사용할수있는jupyter notebook)



- Google Colaboratory
    -https://colab.research.google.com/
    - 다음의 링크에 가셔서 구글 드라이브 로그인을 하시고, 노트' 만들기를 하시면, 콜랩 노트북을 이용할 수 있습니다.

- 단축키
    - ctrl + enter : 실행
    - shift + enter : 실행 후 다음셀로 넘어감

## 표를 다루는 도구 - 판다스
>  pandas는 데이터 처리를 전문적으로 할 수 있는 함수들을 모아놓은 라이브러리  
> In computer programming, **pandas** is a software library written for the Python programming language for data manipulation and analysis. In particular, it offers data structures and operations for manipulating numerical tables and time series. 


- 파일 읽어오기 : **pd.read_csv("/경로/파일명.csv")**
- 표 출력 : **print(데이터.shape)**
- column 선택하기 : **데이터([['칼럼1','칼럼2','칼럼3']])**
- 데이터 표의 column 이름 출력하기 : **print(데이터.columns)**
- 맨 위 5개 관측치 출력하기 : **데이터.head()**

```python
###########################
# 라이브러리 사용
import pandas as pd
 
###########################
# 파일로부터 데이터 읽어오기
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/lemonade.csv'
레모네이드 = pd.read_csv(파일경로)  ## csv로 된 파일을 읽어들이고 데이터를 변수에 담아줌
 
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/boston.csv'
보스턴 = pd.read_csv(파일경로)
 
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/iris.csv'
아이리스 = pd.read_csv(파일경로)
 
###########################
# 데이터의 모양확인
print(레모네이드.shape) ##(number of rows, number of columns)
print(보스턴.shape)
print(아이리스.shape)
 
###########################
# 데이터 칼럼이름 확인
print(레모네이드.columns)
print(보스턴.columns)
print(아이리스.columns)
 
 
###########################
# 독립변수와 종속변수 분리
독립 = 레모네이드[['온도']]
종속 = 레모네이드[['판매량']]
print(독립.shape, 종속.shape)
 
독립 = 보스턴[['crim', 'zn', 'indus', 'chas', 'nox', 
            'rm', 'age', 'dis', 'rad', 'tax',
            'ptratio', 'b', 'lstat']]
종속 = 보스턴[['medv']]
print(독립.shape, 종속.shape)
 
독립 = 아이리스[['꽃잎길이', '꽃잎폭', '꽃받침길이', '꽃받침폭']]
종속 = 아이리스[['품종']]
print(독립.shape, 종속.shape)
 
 
###########################
# 각각의 데이터 확인해보기
print(레모네이드.head())
print(보스턴.head())
print(아이리스.head())
```

## 손실Loss의 의미
```
Epoch 1/10
1/1 [==============================] - 0s 253ms/step - loss: 3959.4944
Epoch 2/10
1/1 [==============================] - 0s 4ms/step - loss: 3950.1233
Epoch 3/10
1/1 [==============================] - 0s 4ms/step - loss: 3943.3352
Epoch 4/10
1/1 [==============================] - 0s 4ms/step - loss: 3937.6582
Epoch 5/10
1/1 [==============================] - 0s 4ms/step - loss: 3932.6233
Epoch 6/10
1/1 [==============================] - 0s 4ms/step - loss: 3928.0129
Epoch 7/10
1/1 [==============================] - 0s 4ms/step - loss: 3923.7058
Epoch 8/10
1/1 [==============================] - 0s 3ms/step - loss: 3919.6267
Epoch 9/10
1/1 [==============================] - 0s 4ms/step - loss: 3915.7258
Epoch 10/10
1/1 [==============================] - 0s 3ms/step - loss: 3911.9661
```
- 3ms/step
    - 각 학습마다 걸린 시간
- loss: 3911.9661 
    - 학습이 끝날때마다 그 시점에 모델이 얼마나 정답에 가까이 맞추고있는지 가리키는 지표
    - "학습의 예측 - 결과"차이의 제곱의 평균이 LOSS
    - 예측이 정답을 모두 맞추게되면 LOSS는 0
    - 0 에 가까워질수록 학습이 잘 된 모델
    - epochs 마다 loss가 0에가까워질때까지 반복해서 학습

## 레모네이드 판매 예측
```python
###########################
# 라이브러리 사용
import tensorflow as tf
import pandas as pd
 
###########################
# 1. 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/lemonade.csv'
레모네이드 = pd.read_csv(파일경로)
레모네이드.head()
# 종속변수, 독립변수를 분리해서 준비
독립 = 레모네이드[['온도']]
종속 = 레모네이드[['판매량']]
print(독립.shape, 종속.shape)
 
###########################
# 2. 모델을 만듭니다.
X = tf.keras.layers.Input(shape=[1])  # input layer - 독립변수의 column이 하나이기 때문에 shape=[1]
Y = tf.keras.layers.Dense(1)(X) # 종속변수의 column이 하나이기 때문에 Dense(1)
model = tf.keras.models.Model(X, Y)
model.compile(loss='mse') # 모델이 학습할 방법 'mse'
 
###########################
# 3. 모델을 학습시킵니다. 
# FIT : 학습
# epochs : 전체 데이터를 몇 번 학습시킬 것인지
# verbose=0 : (option) 학습 loss print 생략
model.fit(독립, 종속, epochs=1000, verbose=0)
model.fit(독립, 종속, epochs=10)
 
###########################
# 4. 모델을 이용합니다. 
print(model.predict(독립)) 
print(model.predict([[15]]))
```