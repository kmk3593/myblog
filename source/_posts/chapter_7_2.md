---
title: "chapter_7_2"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 딥러닝
author: "minkuen"
date: '2022-04-07'
---

# 심층 신경망
- 인공신경망에 층을 여러 개 추가하여 패션 MNIST 데이터셋을 분류한다.
- 동시에 케라스로 심층 신경망을 만들어본다.

- 368p 그림 참고
- 케라스로 API를 사용해 패션 MNIST 데이터셋을 불러온다.


```python
from tensorflow import keras

(train_input, train_target), (test_input, test_target) = keras.datasets.fashion_mnist.load_data()
```

    Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/train-labels-idx1-ubyte.gz
    32768/29515 [=================================] - 0s 0us/step
    40960/29515 [=========================================] - 0s 0us/step
    Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/train-images-idx3-ubyte.gz
    26427392/26421880 [==============================] - 0s 0us/step
    26435584/26421880 [==============================] - 0s 0us/step
    Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/t10k-labels-idx1-ubyte.gz
    16384/5148 [===============================================================================================] - 0s 0us/step
    Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/t10k-images-idx3-ubyte.gz
    4423680/4422102 [==============================] - 0s 0us/step
    4431872/4422102 [==============================] - 0s 0us/step
    

- 이미지의 픽셀값을 0 ~ 255 범위에서 0 ~ 1로 변환
- 28x28 크기의 2차원 배열을 784 크기인 1차원 배열로 펼친다.
- train_test_split() 함수로 훈련 세트와 검증 세트로 나눈다.


```python
from sklearn.model_selection import train_test_split

train_scaled = train_input / 255.0
train_scaled = train_scaled.reshape(-1, 28*28)

train_scaled, val_scaled, train_target, val_target = train_test_split(
    train_scaled, train_target, test_size=0.2, random_state=42)
```

- 입력층과 출력층 사이에 밀집층을 만들 예정이다.
- 은닉층 : 입력층과 출력층 사이에 있는 모든 층 
- 케라스의 Dense 클래스로 다음 내용을 만든다.
  - sigmoid 활성화 함수를 사용한 은닉층
  - softmax 함수를 사용한 출력층

- 층을 추가하는 방법
  - Dense 클래스의 객체 dense1, 2를 만들어 Sequential 클래스에 전달한다.


```python
dense1 = keras.layers.Dense(100, activation='sigmoid', input_shape=(784,))
dense2 = keras.layers.Dense(10, activation='softmax')
```

- dense1이 은닉층이고 100개의 뉴런을 가진 밀집층이다.
  - 활성화 함수를 'sigmoid'로 지정했고 매개변수로 입력의 크기를 (784,)로 지정했다.
- dense2는 출력층이다.
  - 10개의 클래스를 분류하므로 10개의 뉴런을 두었고 활성화 함수는 softmax로 지정했다.

### 심층 신경망
  - 컨셉만 이해하라!
  - 직접 신경망 만들 일은 없고 가져다 쓰기만 하면 된다.

- 앞의 dense1과 dense2 객체를 Sequential 클래스에 추가하여 심층 신경망을 만들 예정이다.


```python
model = keras.Sequential([dense1, dense2])
model.summary()
```

    Model: "sequential"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     dense (Dense)               (None, 100)               78500     
                                                                     
     dense_1 (Dense)             (None, 10)                1010      
                                                                     
    =================================================================
    Total params: 79,510
    Trainable params: 79,510
    Non-trainable params: 0
    _________________________________________________________________
    

- 위와 같이 Sequential 클래스의 객체를 만들 때 여러 개의 층을 추가하려면 층을 리스트로 만들어 전달해야 한다.
- model.summary()로 층에 대한 정보를 얻을 수 있다.
  - 첫 줄에 모델의 이름이 나온다.
  - 이 모델에 들어 있는 층이 순서대로 나열된다.
    - 이 순서는 맨 처음 추가한 은닉층에서 출력층의 순서로 나열된다.
  - 층마다 층 이름, 클래스, 출력 크기, 모델 파라미터 개수가 출력된다.
  - name 매개변수로 이름을 지정하지 않으면 디폴트인 'dense'로 네이밍된다.
  - 출력 크기는 (None,100)인데, 첫 번째 차원은 샘플 개수를 나타낸다.
    - None인 이유는 어떤 배치 크기에도 잘 대응하기 위함이다.
    - 두 번째 차원인 100은 뉴런 개수가 100이며, 따라서 100개의 출력이 나옴을 나타낸다.

### 층을 추가하는 다른 방법
- Sequential 클래스의 생성자 안에서 바로 Dense 클래스의 객체를 만든다.


```python
model = keras.Sequential([
    keras.layers.Dense(100, activation='sigmoid', input_shape=(784,), name='hidden'),   # 층을 쌓아간다
    keras.layers.Dense(10, activation='softmax', name='output')                         # 층을 쌓아간다
], name='패션 MNIST 모델')
model.summary()
```

    Model: "패션 MNIST 모델"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     hidden (Dense)              (None, 100)               78500     
                                                                     
     output (Dense)              (None, 10)                1010      
                                                                     
    =================================================================
    Total params: 79,510
    Trainable params: 79,510
    Non-trainable params: 0
    _________________________________________________________________
    

### 층을 추가하는 다른 방법 2
- Sequential 클래스의 객체를 만들고 이 객체의 add() 메서드를 호출하여 층을 추가한다.


```python
model = keras.Sequential()
model.add(keras.layers.Dense(100, activation='sigmoid', input_shape=(784,)))    # 층을 쌓아간다
model.add(keras.layers.Dense(10, activation='softmax'))                         # 층을 쌓아간다

model.summary()
```

    Model: "sequential_1"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     dense_2 (Dense)             (None, 100)               78500     
                                                                     
     dense_3 (Dense)             (None, 10)                1010      
                                                                     
    =================================================================
    Total params: 79,510
    Trainable params: 79,510
    Non-trainable params: 0
    _________________________________________________________________
    

- 이제 모델을 훈련한다.
  - 반복할 에포크 횟수를 epochs 매개변수로 지정


```python
model.compile(loss='sparse_categorical_crossentropy', metrics='accuracy')
model.fit(train_scaled, train_target, epochs=5)
```

    Epoch 1/5
    1500/1500 [==============================] - 6s 3ms/step - loss: 0.5628 - accuracy: 0.8069
    Epoch 2/5
    1500/1500 [==============================] - 4s 3ms/step - loss: 0.4087 - accuracy: 0.8522
    Epoch 3/5
    1500/1500 [==============================] - 5s 3ms/step - loss: 0.3747 - accuracy: 0.8645
    Epoch 4/5
    1500/1500 [==============================] - 4s 3ms/step - loss: 0.3506 - accuracy: 0.8737
    Epoch 5/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.3344 - accuracy: 0.8784
    




    <keras.callbacks.History at 0x7f5bcb861b50>



- 렐루 함수
  - 층이 많은 신경망일수록 그 효과가 누적되어 학습이 어려워진다.
  - 이를 개선하기 위한 활성화 함수이다. 
  - relu() 함수는 입력이 양수일 그냥 통과시키고, 입력이 음수라면 0으로 만든다. 

- Flatten 클래스
  - 배치 차원을 제외하고 나머지 입력 차원을 모두 일렬로 펼친다.
  - Flatten 클래스를 층처럼 입렬층과 은닉층 사잉에 추가하기 때문에 이를 층이라 부른다. 
  - 다음 코드처럼 입력층 바로 뒤에 추가한다.


```python
model = keras.Sequential()
model.add(keras.layers.Flatten(input_shape=(28,28)))  # 기존 코드 비교
model.add(keras.layers.Dense(100, activation='relu')) # relu 로 변경
model.add(keras.layers.Dense(10, activation='softmax'))

model.summary()
```

    Model: "sequential_2"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     flatten (Flatten)           (None, 784)               0         
                                                                     
     dense_4 (Dense)             (None, 100)               78500     
                                                                     
     dense_5 (Dense)             (None, 10)                1010      
                                                                     
    =================================================================
    Total params: 79,510
    Trainable params: 79,510
    Non-trainable params: 0
    _________________________________________________________________
    

- 훈련 데이터를 다시 준비해서 모델을 훈련한다.


```python
(train_input, train_target), (test_input, test_target) = keras.datasets.fashion_mnist.load_data()

train_scaled = train_input / 255.0

train_scaled, val_scaled, train_target, val_target = train_test_split(
    train_scaled, train_target, test_size=0.2, random_state=42)
```

- 모델을 컴파일하고 훈련한다.


```python
model.compile(loss='sparse_categorical_crossentropy', metrics='accuracy')
model.fit(train_scaled, train_target, epochs=5)
```

    Epoch 1/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.5283 - accuracy: 0.8151
    Epoch 2/5
    1500/1500 [==============================] - 4s 3ms/step - loss: 0.3926 - accuracy: 0.8602
    Epoch 3/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.3562 - accuracy: 0.8713
    Epoch 4/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.3336 - accuracy: 0.8809
    Epoch 5/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.3203 - accuracy: 0.8853
    




    <keras.callbacks.History at 0x7f5bcb762a10>



- 시그모이드 함수를 사용했을 때와 비교하면 성능이 조금 향상되었다.
- 검증 세트에서의 성능도 확인하자.


```python
model.evaluate(val_scaled, val_target)
```

    375/375 [==============================] - 1s 3ms/step - loss: 0.3713 - accuracy: 0.8717
    




    [0.3712655007839203, 0.871749997138977]



- 검증 성능도 향상되었다.


```python
(train_input, train_target), (test_input, test_target) = keras.datasets.fashion_mnist.load_data()

train_scaled = train_input / 255.0

train_scaled, val_scaled, train_target, val_target = train_test_split(
    train_scaled, train_target, test_size=0.2, random_state=42)
```


```python
model.compile(loss='sparse_categorical_crossentropy', metrics='accuracy')
model.fit(train_scaled, train_target, epochs=5)
```

    Epoch 1/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.3094 - accuracy: 0.8890
    Epoch 2/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.2989 - accuracy: 0.8951
    Epoch 3/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.2902 - accuracy: 0.8974
    Epoch 4/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.2825 - accuracy: 0.9018
    Epoch 5/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.2781 - accuracy: 0.9024
    




    <keras.callbacks.History at 0x7f5bcb835d10>




```python
model.evaluate(val_scaled, val_target)
```

    375/375 [==============================] - 1s 1ms/step - loss: 0.4110 - accuracy: 0.8792
    




    [0.41104814410209656, 0.8791666626930237]



### 옵티마이저의 개념
--> Adam 사용하라
--> why Adam? 최고점을 찾기 위해서
  + 스텝방향 & 스템사이즈를 모두 고려한 옵티마이저
  + 스텝방향 : GD, SGD, Momentum, NAG
  + 스텝사이즈 : GD, SGD, Adagrad, RMSProp

- 하이퍼 파라미터는 사람이 지정해야 하는 파라미터
- 신경망에는 특히 하이퍼 파라미터가 많다.
- 은닉층의 뉴런 개수도 하이퍼 파라미터이다.
- compile() 에서는 케라스의 기본 하강법 알고리즘인 RMSprop을 사용했다.
  - 케라스는 다양한 종류의 경사 하강법 알고리즘을 제공한다.
  - 이들을 '옵티마이저'라고 부른다.

### 옵티마이저 
- 381p
- SGD 옵티마이저를 사용하려면 compile() 메서드의 optimizer 매개변수를 'sgd'로 지정


```python
model.compile(optimizer='sgd', loss='sparse_categorical_crossentropy', metrics='accuracy')
```

- 'sgd' 문자열은 이 클래스의 기본 설정 매개변수로 생성한 객체와 동일하다.
- 다음 코드는 위의 코드와 정확히 동일하다.


```python
sgd = keras.optimizers.SGD()
model.compile(optimizer=sgd, loss='sparse_categorical_crossentropy', metrics='accuracy')
```

- 382p
- learning_rate = 0.1
  - 만약 SGD 클래스의 학습률 기본값이 0.01일 때 이를 바꾸고 싶다면 다음와 같이 지정한다.
- 랜덤서치, 그리드서치
- 딥러닝에서도 하이퍼파라미터 튜닝


```python
sgd = keras.optimizers.SGD(learning_rate = 0.1)
```

- 기본 경사 하강법 옵티마이저는 모두 SGD 클래스에서 제공한다.
- SGD 클래서의 momentum 매개변수의 기본값은 0이다. 보통 0.9이상을 지정한다.
- 다음처럼 SGD 클래스의 nesterov 매개변수를 기본값 False 에서 True로 바꾸면 네스테로프 모멘텀 최적화를 사용한다.
  - 테스테로프 모멘텀은 모멘텀 최적화를 2번 반복하여 구현한다.
  - 대부분의 경우 네스테로프 모멘텀 최적화가 기본 확률적 경사 하강법보다 더 나은 성능을 제공한다.


```python
sgd = keras.optimizers.SGD(momentum = 0.9, nesterov = True)
```

- 적응적 학습률
  - 모델이 최적점에 가까이 갈수록 학습률을 낮출 수 있다.
  - 이렇게 하면 안정적으로 최적점에 수렴할 가능성이 높다.
  - 이런 학습률을 적응적 학습률이라고 한다.

- Adagrad() 클래스
  - 적응적 학습률을 사용하는 대표적인 옵티마이저이다.
  - optimizer 매개변수에서 지정할 수 있다.
  - optimizer 매개변수의 기본값이 바로 rmsprop이다.


```python
adagrad = keras.optimizers.Adagrad()
model.compile(optimizer=adagrad, loss='sparse_categorical_crossentropy', metrics='accuracy')
```

- RMSprop() 클래스
  - 적응적 학습률을 사용하는 대표적인 옵티마이저이다.
  - optimizer 매개변수에서 지정할 수 있다.
  - optimizer 매개변수의 기본값이 바로 rmsprop이다.


```python
rmsprop = keras.optimizers.RMSprop()
model.compile(optimizer=rmsprop, loss='sparse_categorical_crossentropy', metrics='accuracy')
```

- 다만, Adam을 사용하는 것이 더 좋다.
- Adam
  - 모멘텀 최적화와 RMSprop의 장점을 접목한 것이 Adam이다.
  - 적응적 학습률을 사용하는 이 3개의 클래스는 learning_rate 매개변수의 기본값을 0.001로 두고 사용한다.

- Adam 클래스의 매개변수 기본값을 사용해 패션 MNIST 모델을 훈련해본다.
- 일단 모델을 다시 생성한다.


```python
model = keras.Sequential()
model.add(keras.layers.Flatten(input_shape=(28,28)))  # 기존 코드 비교
model.add(keras.layers.Dense(100, activation='relu')) # relu 로 변경
model.add(keras.layers.Dense(10, activation='softmax'))
```

- compile() 메서드의 optimizer를 'adam'으로 설정하고 5번의 에포크 동안 훈련한다.


```python
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics='accuracy')
model.fit(train_scaled, train_target, epochs=5)
model.evaluate(val_scaled, val_target)
```

    Epoch 1/5
    1500/1500 [==============================] - 4s 2ms/step - loss: 0.5293 - accuracy: 0.8155
    Epoch 2/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.3980 - accuracy: 0.8571
    Epoch 3/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.3542 - accuracy: 0.8713
    Epoch 4/5
    1500/1500 [==============================] - 4s 3ms/step - loss: 0.3287 - accuracy: 0.8798
    Epoch 5/5
    1500/1500 [==============================] - 3s 2ms/step - loss: 0.3081 - accuracy: 0.8867
    375/375 [==============================] - 1s 2ms/step - loss: 0.3296 - accuracy: 0.8806
    




    [0.32961416244506836, 0.8805833458900452]



- 결과를 보면 기본 RMSprop을 사용했을 때와 거의 같은 성능을 보인다.
- 검증 세트에서의  성능도 확인한다.


```python
model.evaluate(val_scaled, val_target)
```

    375/375 [==============================] - 1s 3ms/step - loss: 0.3296 - accuracy: 0.8806
    




    [0.32961416244506836, 0.8805833458900452]



- 환경마다 차이가 있을 수 있지만 여기서는 기본 RMSprop보다 조금 더 나은 성능을 보인다.

- Reference : 혼자 공부하는 머신러닝 + 딥러닝 
