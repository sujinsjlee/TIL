---
title: "Tensorflow - Python (4) 히든레이어"
categories:
  - Tensorflow
tags:
  - Tensorflow
---

## Hidden Layer
- perceptron하나로 연결된 모델이아닌 신경망을 더 깊게만드는 것
- Hidden Layer
    - 독립변수와 종속변수사이에 추가되는 layer
    - input layer 과 output layer사이에 추가되는 layer

- Hidden Layer 만드는 이유
    - 보다 복잡한 모델을 사용하여 데이터를 학습하는 것
    - 복잡한 모델은 복잡한 수식과 동의어
    - 히든레이어를 사용한다는 것은 **결과를 더 정확히 예측할 수 있는 함수(모델)를 만들게 된다는 것**
    - 구조를 복잡하게 함으로써 더 복잡한 문제를 풀 수 있게 됩니다.  물론 구조를 복잡하게 되면 시간이 좀 더 걸리겠죠. 처리속도의 손실을 통해 정확도를 높이는 거에요.

- layer (node) 를 몇개 추가해야 적절한 것인지에 대한 기준
    - loss가 낮아지는 만큼 추가


## 보스턴 집값 예측 (실습)

```python
##########################
# 라이브러리 사용
import tensorflow as tf
import pandas as pd
 
###########################
# 1.과거의 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/boston.csv'
보스턴 = pd.read_csv(파일경로)
 
# 종속변수, 독립변수
독립 = 보스턴[['crim', 'zn', 'indus', 'chas', 'nox', 
            'rm', 'age', 'dis', 'rad', 'tax',
            'ptratio', 'b', 'lstat']]
종속 = 보스턴[['medv']]
print(독립.shape, 종속.shape)
 
###########################
# 2. 모델의 구조를 만듭니다
X = tf.keras.layers.Input(shape=[13])
H = tf.keras.layers.Dense(10, activation='swish')(X) # 10개의 노드를 만들 것, hidden layer의 activation함수는 swish
Y = tf.keras.layers.Dense(1)(H) # X가 아닌 H를 대입
model = tf.keras.models.Model(X, Y)
model.compile(loss='mse')
 
# 모델 구조 확인
model.summary() # summary() 하면 layer개수 정보에대한 자세한 출력이나옵니다.
 
###########################
# 3.데이터로 모델을 학습(FIT)합니다.
model.fit(독립, 종속, epochs=100)
 
###########################
# 4. 모델을 이용합니다
print(model.predict(독립[:5]))
print(종속[:5])
 
###########################
# 모델의 수식 확인
print(model.get_weights())
```

- **model.summary()**

```
Model: "model"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
input_1 (InputLayer)         [(None, 13)]              0         
_________________________________________________________________
dense (Dense)                (None, 10)                140       
_________________________________________________________________
dense_1 (Dense)              (None, 1)                 11        
=================================================================
Total params: 151
Trainable params: 151
Non-trainable params: 0
_________________________________________________________________
```
- InputLayer : 입력layer는 13개의 변수를 받음
- dense_2 : 13개의 입력을 받아서 10개의 output을 만드는 layer
- dense_3 : 10개의 입력을 받아서 1개의 output을 만드는 layer

- Params # : 컴퓨터가 학습하는 가중치
    - 140 : 13개의 입력을 받아서 bias하나 추가되니까 수식마다 14개. output이 10개니까 14 * 10 == 140개
    - 11 : 10개의 입력을 받아서 1개의 출력을 만드니까 수식이 10개고 1개의 bias가 추가되니까 11개의 가중치

## 아이리스 품종 (실습)
```python
###########################
# 라이브러리 사용
import tensorflow as tf
import pandas as pd
 
###########################
# 1.과거의 데이터를 준비합니다.
파일경로 = 'https://raw.githubusercontent.com/blackdew/tensorflow1/master/csv/iris.csv'
아이리스 = pd.read_csv(파일경로)
 
# 원핫인코딩
아이리스 = pd.get_dummies(아이리스)
 
# 종속변수, 독립변수
독립 = 아이리스[['꽃잎길이', '꽃잎폭', '꽃받침길이', '꽃받침폭']]
종속 = 아이리스[['품종_setosa', '품종_versicolor', '품종_virginica']]
print(독립.shape, 종속.shape)
 
###########################
# 2. 모델의 구조를 만듭니다
X = tf.keras.layers.Input(shape=[4])
H = tf.keras.layers.Dense(8, activation="swish")(X) # node(layer)개수는 8개
H = tf.keras.layers.Dense(8, activation="swish")(H)
H = tf.keras.layers.Dense(8, activation="swish")(H)
Y = tf.keras.layers.Dense(3, activation='softmax')(H)
model = tf.keras.models.Model(X, Y)
model.compile(loss='categorical_crossentropy',
              metrics='accuracy')
 
# 모델 구조 확인
model.summary()
 
###########################
# 3.데이터로 모델을 학습(FIT)합니다.
model.fit(독립, 종속, epochs=100)
 
###########################
# 4. 모델을 이용합니다
print(model.predict(독립[:5]))
print(종속[:5])
```