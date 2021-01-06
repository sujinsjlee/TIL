---
title: "Tensorflow - Python (2) 보스턴 집 값 예측"
categories:
  - Tensorflow
tags:
  - Tensorflow
---
## 보스턴 집 값 예측
- 각각의 행 : town
- 열 : 해당 town에 영향을 미치는 변수
- **medv** : 집값의 중간값
    - 첫번째 행의 medv 24 : 해당 town의 주택 값의 중간값이 24
    - 이 값이 클 수록 비싼 주택이 많은 지역이 됩니다.
- crim : 범죄율
- Chas : 강변 (가까우면 1 아니면 0)
- RM : 평균 방수
- AGE : 노후주택 비율
- TAX : 재산세 세율
- PTRATIO : 학생/교사 비율
- LSTAT : 하위계층 비율


> **y = w1x1 + w2x2 + w3x3 + ... + b**  
> 아래 코드에서 Dense() layer는 위 수식을 만들어 냅니다.  
> 컴퓨터는 학습하는 과정에서 입력데이터를 보고 위 수식의 w와 b를 찾아냅니다.  
> 위 수식 == 인공 신경망에서 뉴런 == **Persceptron == 퍼셉트론**  
> x : 독립변수  
> y : 종속변수  
> **Weight 가중치**  
> **Bias 편향**  


- 딥러닝데이터를 가지고 스스로 학습한다는 것은 신기하다
- 아하! 수식을 만들어놓고 종속변수의 값을 가장 근접하게 만들도록 가중치를 찾는 것이구나!



## 소스 코드
```python
###########################
# 라이브러리 사용
import tensorflow as tf
import pandas as pd
 
###########################
# 1.과거의 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/boston.csv'
보스턴 = pd.read_csv(파일경로)
print(보스턴.columns)
보스턴.head()
 
# 독립변수, 종속변수 분리 
독립 = 보스턴[['crim', 'zn', 'indus', 'chas', 'nox', 'rm', 'age', 'dis', 'rad', 'tax',
            'ptratio', 'b', 'lstat']]
종속 = 보스턴[['medv']]
print(독립.shape, 종속.shape)
 
###########################
# 2. 모델의 구조를 만듭니다
X = tf.keras.layers.Input(shape=[13])  # 독립변수 개수
Y = tf.keras.layers.Dense(1)(X)  # 종속변수 개수
model = tf.keras.models.Model(X, Y)
model.compile(loss='mse')
 
###########################
# 3.데이터로 모델을 학습(FIT)합니다.
model.fit(독립, 종속, epochs=1000, verbose=0)
model.fit(독립, 종속, epochs=10)
 
###########################
# 4. 모델을 이용합니다
print(model.predict(독립[5:10])) #python : **슬라이싱**  독립변수의 5번째부터 10번째까지 예측
# 종속변수 확인
print(종속[5:10])
 
###########################
# 모델의 수식 확인
print(model.get_weights()) # bias 값을 print된 결과에서 array에서 볼 수 있음
```