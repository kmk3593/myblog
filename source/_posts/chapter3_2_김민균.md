---
title: "chapter3_2"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
author: "minkuen"
date: '2022-03-30'
---


### 데이터 준비하기


```python
import numpy as np

perch_length = np.array(
    [8.4, 13.7, 15.0, 16.2, 17.4, 18.0, 18.7, 19.0, 19.6, 20.0, 
     21.0, 21.0, 21.0, 21.3, 22.0, 22.0, 22.0, 22.0, 22.0, 22.5, 
     22.5, 22.7, 23.0, 23.5, 24.0, 24.0, 24.6, 25.0, 25.6, 26.5, 
     27.3, 27.5, 27.5, 27.5, 28.0, 28.7, 30.0, 32.8, 34.5, 35.0, 
     36.5, 36.0, 37.0, 37.0, 39.0, 39.0, 39.0, 40.0, 40.0, 40.0, 
     40.0, 42.0, 43.0, 43.0, 43.5, 44.0]
     )
perch_weight = np.array(
    [5.9, 32.0, 40.0, 51.5, 70.0, 100.0, 78.0, 80.0, 85.0, 85.0, 
     110.0, 115.0, 125.0, 130.0, 120.0, 120.0, 130.0, 135.0, 110.0, 
     130.0, 150.0, 145.0, 150.0, 170.0, 225.0, 145.0, 188.0, 180.0, 
     197.0, 218.0, 300.0, 260.0, 265.0, 250.0, 250.0, 300.0, 320.0, 
     514.0, 556.0, 840.0, 685.0, 700.0, 700.0, 690.0, 900.0, 650.0, 
     820.0, 850.0, 900.0, 1015.0, 820.0, 1100.0, 1000.0, 1100.0, 
     1000.0, 1000.0]
     )
```

- 훈련 세트와 테스트 세트로 나눈다.


```python
from sklearn.model_selection import train_test_split

train_input, test_input, train_target, test_target = train_test_split( 
    perch_length, perch_weight, random_state = 42
)

train_input.shape, test_input.shape, train_target.shape, test_target.shape
```




    ((42,), (14,), (42,), (14,))



- 훈련 세트와 테스트 세트를 2차원 배열로 변경


```python
train_input = train_input.reshape(-1, 1)
test_input = test_input.reshape(-1, 1)

print(train_input.shape, test_input.shape)
```

    (42, 1) (14, 1)
    

### 모델 만들기


```python
from sklearn.neighbors import KNeighborsRegressor

# knn 클래스 불러오기
knr = KNeighborsRegressor(n_neighbors=3)

# 모형학습
knr.fit(train_input, train_target)

# 테스트 점수 확인하자
#knr.score(test_input, test_target)
```




    KNeighborsRegressor(n_neighbors=3)



### 예측
- 혼자 공부하는 머신러닝 + 딥러닝
  -  p132


```python
# 어떤 숫자로 바꿔도 결과는 동일하다
print(knr.predict([[50]]))  
```

    [1033.33333333]
    

### 시각화


```python
import matplotlib.pyplot as plt

# 50cm 농어의 이웃을 구하라!
distances, indexes = knr.kneighbors([[50]])

# 훈련 세트의 산점도를 구하라

plt.scatter(train_input, train_target)
plt.scatter(train_input[indexes], train_target[indexes], marker = 'D')
plt.scatter(50, 1033, marker='^')
plt.show()
```


    
![png](/images/chapter3_2_김민균/output_11_0.png)
    


- [과제] 위 시각화를 객체 지향으로 변경한다!


```python
import matplotlib.pyplot as plt

# 50cm 농어의 이웃을 구하라!
distances, indexes = knr.kneighbors([[50]])

# 훈련 세트의 산점도를 구하라
fig, ax = plt.subplots()
ax.scatter(train_input, train_target)
ax.scatter(train_input[indexes], train_target[indexes], marker = 'D')
ax.scatter(50, 1033, marker='^')
plt.show()

# 아래 코드를 참고함.
""" 
import matplotlib.pyplot as plt

# 객체 지향으로 변경
fig, ax = plt.subplots()
ax.scatter(perch_length, perch_weight)
ax.set_xlabel("length")
ax.set_xlabel("weight")

plt.show()
"""
```


    
![png](/images/chapter3_2_김민균/output_13_0.png)
    





    '\nimport matplotlib.pyplot as plt\n\n# 객체 지향으로 변경\nfig, ax = plt.subplots()\nax.scatter(perch_length, perch_weight)\nax.set_xlabel("length")\nax.set_xlabel("weight")\n\nplt.show()\n'



- 머신러닝 모델은 주기적으로 훈련해야 한다. (135p)
  + MLOps (Machine Learning & Operations)
  + 최근에 각광받는 데이터 관련 직업 필수 스킬!
  + 입사와 함께 공부시작 (데이터 분석가, 머신러닝 엔지니어, 데이터 싸이언티스트 희망자)

### 선형회귀 (머신러닝)
- 평가지표 확신이 더 중요! R2 점수, MAE, MSE,...
- 5가지 가정들...
- 잔차의 정규성
- 등분산성, 다중공선성, etc...
- 종속변수 ~ 독립변수간의 "인간관계"를 찾는 과정...


```python
from sklearn.linear_model import LinearRegression

lr = LinearRegression()

# 선형 회귀 모델 훈련
lr.fit(train_input, train_target)

# 50 cm 농어 예측
print(lr.predict([[200]]))
```

    [7094.41034777]
    


```python
plt.scatter(train_input, train_target)
plt.scatter(train_input[indexes], train_target[indexes], marker = 'D')
plt.scatter(200, 7094, marker='^')
plt.show()
```


    
![png](/images/chapter3_2_김민균/output_17_0.png)
    


### 회귀식을 찾기
- coef_  : 기울기
- intercept_ : 상수


```python
# 기울기,  상수
print(lr.coef_, lr.intercept_)
```

    [39.01714496] -709.0186449535477
    

- 기울기 : 계수 = 가중치(딥러닝)


```python
plt.scatter(train_input, train_target)

# 15~50 까지의 1차 방정식 그래프를 그린다.
plt.plot([15, 50], 
         [15 * lr.coef_ + lr.intercept_,
          50 * lr.coef_ + lr.intercept_,
          ])
plt.scatter(50, 1241.8, marker='^')
plt.show()
```


    
![png](/images/chapter3_2_김민균/output_21_0.png)
    


- 모형 평가 (138p)
  + 과소 적합이 됨
  

# 다항회귀의 필요성
- 치어를 생각해보자
- 치어가 1cm


```python
print(lr.predict([[1]]))
```

    [-670.00149999]
    

- (140p) 1차 방정식을 2차방정식으로 만드는 과정이 나옴
- 넘파이 브로드캐스팅
   + 배열의 크기가 동일하면 상관 없음
   + 배열의 크기가 다른데, 연산을 할 때, 브로드캐스팅 원리가 적용
   + 브로드캐스팅 튜토리얼, 뭘 찾아서, 추가적 공부를 해야 함(분석가 지망, ai분야 지망)


```python
train_poly = np.column_stack((train_input ** 2, train_input))
test_poly = np.column_stack((test_input ** 2, test_input))

print(train_poly.shape, test_poly.shape)
```

    (42, 2) (14, 2)
    


```python
lr = LinearRegression()

lr.fit(train_poly, train_target)

print(lr.predict([[50 ** 2, 50]]))      
```

    [1573.98423528]
    


```python
# 기울기,  상수
print(lr.coef_, lr.intercept_)
```

    [  1.01433211 -21.55792498] 116.0502107827827
    

- 이 모델은 다음과 같은 그래프를 학습했다.
  - 무게 = 1.01 x 길이^2 - 21.6 x 길이 + 116.05

- KNN의 문제점
  + 농어의 길이가 커져도 무게는 동일함 (현실성 제로)
- 단순 선형회귀(1차 방정식)의 문제점
  + 치어(1cm)의 무게가 음수로 나옴 (현실성 제로)
- 다항 회귀(2차 방정식)으로 변경
  + 현실성 있음

- 이런 방정식을 다항싱(polynomial)이라 부르며 다항식을 사용한 선형 외귀를 다항 회귀(polynomial regression)이라 부른다.
- 이를 이용하여 이전과 동일하게 훈련 세트의 산점도에 그래프로 그려보자.


```python
# 구간별 직선을 그리기 위해 15 에서 49까지 정수 배열을 만든다.
point = np.arange(15, 50)

# 훈련 세트의 산점도를 그린다.
plt.scatter(train_input, train_target)

# 15에서 49까지 2차 방정식 그래프를 그린다.
plt.plot(point, 1.01*point**2 - 21.6*point + 116.05)

#50cm 농어 데이터
plt.scatter(50, 1574, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter3_2_김민균/output_32_0.png)
    


- 앞선 단순 선형 회귀 모델보다 훨씬 나은 그래프가 그려졌다.
- 이제 훈련 세트와 테스트 세트의 R^2 점수를 평가한다.


```python
print(lr.score(train_poly, train_target))
print(lr.score(test_poly, test_target))
```

    0.9706807451768623
    0.9775935108325122
    

- 두 세트의 점수가 높아졌다. 좋은 결과다.
- 하지만 여전히 테스트 세트의 점수가 조금 더 높다.
- 과소적합이 아직 남아 있는 듯 하다. 3-3 에서 이를 해결해보자

### 전체 소스 코드
- 다음을 참고하라 : bit.ly/hg-03-2


```python
import numpy as np

perch_length = np.array(
    [8.4, 13.7, 15.0, 16.2, 17.4, 18.0, 18.7, 19.0, 19.6, 20.0, 
     21.0, 21.0, 21.0, 21.3, 22.0, 22.0, 22.0, 22.0, 22.0, 22.5, 
     22.5, 22.7, 23.0, 23.5, 24.0, 24.0, 24.6, 25.0, 25.6, 26.5, 
     27.3, 27.5, 27.5, 27.5, 28.0, 28.7, 30.0, 32.8, 34.5, 35.0, 
     36.5, 36.0, 37.0, 37.0, 39.0, 39.0, 39.0, 40.0, 40.0, 40.0, 
     40.0, 42.0, 43.0, 43.0, 43.5, 44.0]
     )
perch_weight = np.array(
    [5.9, 32.0, 40.0, 51.5, 70.0, 100.0, 78.0, 80.0, 85.0, 85.0, 
     110.0, 115.0, 125.0, 130.0, 120.0, 120.0, 130.0, 135.0, 110.0, 
     130.0, 150.0, 145.0, 150.0, 170.0, 225.0, 145.0, 188.0, 180.0, 
     197.0, 218.0, 300.0, 260.0, 265.0, 250.0, 250.0, 300.0, 320.0, 
     514.0, 556.0, 840.0, 685.0, 700.0, 700.0, 690.0, 900.0, 650.0, 
     820.0, 850.0, 900.0, 1015.0, 820.0, 1100.0, 1000.0, 1100.0, 
     1000.0, 1000.0]
     )

from sklearn.model_selection import train_test_split

# 훈련 세트와 테스트 세트로 나눕니다
train_input, test_input, train_target, test_target = train_test_split(
    perch_length, perch_weight, random_state=42)
# 훈련 세트와 테스트 세트를 2차원 배열로 바꿉니다
train_input = train_input.reshape(-1, 1)
test_input = test_input.reshape(-1, 1)

from sklearn.neighbors import KNeighborsRegressor

knr = KNeighborsRegressor(n_neighbors=3)
# k-최근접 이웃 회귀 모델을 훈련합니다
knr.fit(train_input, train_target)

print(knr.predict([[50]]))

import matplotlib.pyplot as plt

# 50cm 농어의 이웃을 구합니다
distances, indexes = knr.kneighbors([[50]])

# 훈련 세트의 산점도를 그립니다
plt.scatter(train_input, train_target)
# 훈련 세트 중에서 이웃 샘플만 다시 그립니다
plt.scatter(train_input[indexes], train_target[indexes], marker='D')
# 50cm 농어 데이터
plt.scatter(50, 1033, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

print(np.mean(train_target[indexes]))
print(knr.predict([[100]]))

# 100cm 농어의 이웃을 구합니다
distances, indexes = knr.kneighbors([[100]])

# 훈련 세트의 산점도를 그립니다
plt.scatter(train_input, train_target)
# 훈련 세트 중에서 이웃 샘플만 다시 그립니다
plt.scatter(train_input[indexes], train_target[indexes], marker='D')
# 100cm 농어 데이터
plt.scatter(100, 1033, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

from sklearn.linear_model import LinearRegression

lr = LinearRegression()
# 선형 회귀 모델 훈련
lr.fit(train_input, train_target)

# 50cm 농어에 대한 예측
print(lr.predict([[50]]))

print(lr.coef_, lr.intercept_)

# 훈련 세트의 산점도를 그립니다
plt.scatter(train_input, train_target)
# 15에서 50까지 1차 방정식 그래프를 그립니다
plt.plot([15, 50], [15*lr.coef_+lr.intercept_, 50*lr.coef_+lr.intercept_])
# 50cm 농어 데이터
plt.scatter(50, 1241.8, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

print(lr.score(train_input, train_target))
print(lr.score(test_input, test_target))

train_poly = np.column_stack((train_input ** 2, train_input))
test_poly = np.column_stack((test_input ** 2, test_input))

print(train_poly.shape, test_poly.shape)

lr = LinearRegression()
lr.fit(train_poly, train_target)

print(lr.predict([[50**2, 50]]))

print(lr.coef_, lr.intercept_)

# 구간별 직선을 그리기 위해 15에서 49까지 정수 배열을 만듭니다
point = np.arange(15, 50)
# 훈련 세트의 산점도를 그립니다
plt.scatter(train_input, train_target)
# 15에서 49까지 2차 방정식 그래프를 그립니다
plt.plot(point, 1.01*point**2 - 21.6*point + 116.05)
# 50cm 농어 데이터
plt.scatter([50], [1574], marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

print(lr.score(train_poly, train_target))
print(lr.score(test_poly, test_target))
```

    [1033.33333333]
    


    
![png](/images/chapter3_2_김민균/output_37_1.png)
    


    1033.3333333333333
    [1033.33333333]
    


    
![png](/images/chapter3_2_김민균/output_37_3.png)
    


    [1241.83860323]
    [39.01714496] -709.0186449535477
    


    
![png](/images/chapter3_2_김민균/output_37_5.png)
    


    0.939846333997604
    0.8247503123313558
    (42, 2) (14, 2)
    [1573.98423528]
    [  1.01433211 -21.55792498] 116.0502107827827
    


    
![png](/images/chapter3_2_김민균/output_37_7.png)
    


    0.9706807451768623
    0.9775935108325122
    

- Reference : 혼자 공부하는 머신러닝 + 딥러닝
