---
title: "chapter_8_1"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 인공신경망
author: "minkuen"
date: '2022-04-08'
---

# 합성곱 신경망
- 코드보다는 용어 정리가 중요하다
- 더 나은 정확도를 위한 발전 과정
  - 로지스틱 회귀 (일반 ML 모형) : 81%
  - 인공신경망 (딥러닝 초기 모형) : 87%
  - 합성곱 (Convolution, CNN)

- 합성곱 (CNN)
  - 이미지의 특성을 뽑아내는 과정
  - 합성곱에서는 뉴런이 입력층 위를 이동하면서 출력을 만든다. = 도장을 연상하라 
  - 합성곱 층의 뉴런에 있는 가중치 개수는 하이퍼 파라미터이다.
    + 발전사 : alexnet -> resnet -> efficientnet
    + 채널, 이미지의 너비, 크기 (파라미터 튜닝)
    + Vision Transformer
  - 비디오
    + 객체인식(Object Detection)
    + Yolo 논문

- RNN / LSTM (자연어 처리)
  + 구글 2017년 Transformer (논문)

- 필터 (filter)
  - 합성곱에서의 뉴런
    - 뉴런 개수를 이야기할 때 필터라 칭한다.
    - 합성곱에서는 완전 연결 신경망과 달리 뉴런을 필터라 부른다.
  - 혹은 커널(kernel)이라 부른다.
    - 입력에 곱해지는 가중치를의미할 때 커널이라 부른다.

### 합성곱의 장점
- 기존 : 1차원 배열에서만 연산이 가능
- 2차원 배열에도 연산을 할 수 있도록 구현
  + 입력이 2차원 배열이 되므로 필터도 2차원이다.
  + 선형대수를 공부해야 하나요??



```python
from tensorflow import keras
keras.layers.Conv2D(10,                   # 필터(즉, 도장)의 개수
                    kernel_size=(3,3),    # 필터에 사용할 커널의 크기
                    activation = 'relu')  # 활성화 함수 지정
```




    <keras.layers.convolutional.Conv2D at 0x7f6c99df5c90>



### 패딩 (padding)
- 입력 배열의 주위를 가상의 원소로 채우는 것.
- 실제 입력값이 아니기 때문에 패딩은 0으로 채운다. 
- 실제 값은 0으로 채워져 있기에 계산에 영향을 미치지 않는다.
  + 세임 패딩 (same padding) : 입력 주위에 0으로 패딩 하는 것
  + 밸리드 패딩 (valid padding) : 패딩 없이 순수한 입력 배열에서만 합성곱하여 특성 맵을 마드는 것

### 패딩의 목적
- 배열의 크기를 조정하더라도 이미지 원 특성이 손실되는 것을 방지하는 것

### 스트라이드 (stride)
- 기존에 합성곱 연산은 좌우, 위아래로 한 칸씩 이동했다.
  - 두 칸씩 건너뛸 수도 있다.
  - 이런 이동의 크기를 '스트라이드'라고  한다.
- 두 칸씩 이동하면 특성 맵의 크기가 더 작아진다.
  - 커널 도장을 찍는 횟수가 줄어들기 때문.
- 디폴트는 1칸 이동이다.


```python
keras.layers.Conv2D(10,                         # 필터(즉, 도장)의 개수
                   kernel_size=(3,3),          # 필터에 사용할 커널의 크기
                   activation='relu',          # 활성화 함수 지정
                   padding = 'same',           # 세임 패딩
                   strides = 1)                # 1칸씩 이동
```




    <keras.layers.convolutional.Conv2D at 0x7f6c992ba8d0>



### 풀링 (pooling)
- 값을 추출
- 100 x 100 이미지 --> (수치로) 주요 이미지의 특성만 뽑은 후, 원 이미지와 같게 만듬 (50 x 50)
- 합성곱 층에서 만든 특성 맵의 가로세로 크기를 줄이는 역할을 수행한다.
  - 특성맵의 크기를 줄이지는 않는다.
- 합성곱처럼 입력 위를 지나가면서 도장을 찍는다.
  - 하지만, 풀링에는 가중치가 없다.
- 최대 풀링 (max pooling)
  - 도장을 찍은 영역에서 가장 큰 값을 고른다.
- 평균 풀링 (average pooling)
  - 도장을 찍은 영역에서 평균값을 계산한다.
- 특성 맵이 여러 개라면 동일한 작업을 반복한다.
  - 즉, 10개의 특성 맵이 있다면 풀링을 거친 특성맵도 10개가 된다.
- 풀링 영역은 풀링의 크기만큼 이동한다.
  - 즉, 겹치지 않고 이동한다.
  - 풀링의 크기가 (2,2)이면 가로세로 두 칸씩 이동한다.
  - 풀링은 가중치가 없고 풀링 크기와 스트라이드가 같다.



```python
keras.layers.MaxPooling2D(2,                 # 풀링의 크기. 대부분은 2로 둔다.
                          strides=2,         # 2칸씩 이동. 풀링의 크기와 같게 설정된다.
                          padding='valid')   # 풀링은 패딩을 하지 않으므로 'valid'로 지정.
```




    <keras.layers.pooling.MaxPooling2D at 0x7f6c99253e90>



- 기억할 점
  - 풀링은 가로세로 방향으로만 진행한다.
  - 특성 맵의 개수는 변하지 않고 그대로이다.

### 합성곱 신경망의 전체 구조
- p437
- 1단계 : 이미지 데이터 입력
- 2단계 : 합성곱 층
  + (1) kernel_size + padding
  + (2) 활성화 함수 적용
  + (3) 각각의 특성맵을 산출
- 3단계 : 풀링층
  + (1) Max Pooling : 최댓값 추출
  + (2) 최종 특성맵
- 위 과정을 계속 반복하는 것이 CNN 알고리즘
- 4단계 : 밀집층 (Fully Connected Layer)
  + Chapter 7장
  + 3차원 배열을 1차원으로 펼친다. (Flatten 클래스)
  + 출력층의 입력이 된다.
- 5단계 : 분류 예측값을 산출 (Softmax 활성화 함수)
  + 지정한 활성화 함수를 거쳐 최종 예측 확률이 된다.

주요 키워드 : 사전학습(Pretrained) / 전이학습 (Transfer Learning) / 파인 튜닝(Fine Tuning)
- 다른 사람이 작성한 학습 코드를 사용한다.
- 파인 튜닝 : 미세 조정하는 것이다.
  - 캐글 경진대회에서 주로 사용.

- Reference : 혼자 공부하는 머신러닝 + 딥러닝