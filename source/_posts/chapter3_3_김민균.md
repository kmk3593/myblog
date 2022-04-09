---
title: "chapter3_3"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 알고리즘
author: "minkuen"
date: '2022-03-31'
---

# 특성 공학과 규제
- 선형 회귀는 특성이 많을수록 효과가 좋아진다.
  - 무게와 길이뿐만 아니라 높이와 두께도 활용해보자.
  - 사이킷런의 PolynomialFeatures  클래스를 사용한다.

### ***포인트***
- 모델에 규제를 추가함
  + 모형의 과대적합을 방지하기 위해!
    - 훈련 데이터는 예측 성능이 좋고! 테스트 데이터는 예측성능이 떨어지는 현상
  + 릿지, 라쏘 회귀 (중요도 하)
- 하이퍼 파라미터 (개념 이해 중요!)
  - 머신러닝 모델이 학습할수 없고 사람이 알려줘야 하는 파라미터 (161p 참고)
  + 실무에서는 그렇게 큰 의미가 없음
  + 이유 : 가성비가 떨어짐 (작업시간 대비 성능 보장이 안 됨)


### 하이퍼 파라미터
- 기본 모델에서 과대적합이 발생함
- 모델의 성능을 높여주기 위해 여러 옵션을 선택 및 값 조정
  + 문제 : 항상 선응이 보장이 안됨
  + 모델마다 하이퍼 파라미터 새팅하는 방법이 다 다름 (종류가 제 각각)
  + scikit-learn 라이브러리 내 모델의 갯수가 103개
  + 어떤 모델은 하이퍼 파라미터 새팅 위해 필요한 매개 변수가 1개인 경우도 있음
  + 어떤 모델은 하이퍼 파라미터의 매개변수가 80개가 넘어가는 것도 있음
    - 하이퍼 파라미터 기존에 세팅되어 있는대로 사용 권유 (조건: 그 모델에 잘 모르면!!)

### 다중 회귀 (multiple regression)
- 여러 개의 특성을 사용한 선형 회귀를 다중 회귀라고 부른다.

### 특성 공학(feagure engineering)
- 기존의 각 특성을 서로 곱해서 또 다른 특성을 만들 수 있다.
- 예를 들어, '농어 길이 x 농어 높이'를 새로운 특성으로 삼을 수 있다.
- 이렇게 기존의 특성을 사용해 새로운 특성을 뽑아내는 작업을 특성 공학이라고 부른다.

### 데이터 준비
- 이전과 달리 농어의 특성 3개를 사용한다.
- 판다스를 이용하여 간편하게 데이터를 입력한다.
- 판다스(pandas)는 데이터 분석 라이브러리이다.
- 데이터프레임(dataframe)은 판다스의 핵심 데이터 구조이다.
- 판다스 데이터 프레임을 만들기 위해 많이 사용하는 파일은 CSV 파일이다.



- 다음 주소와 read_csv()함수로 파일을 읽어낸다. :https://bit.ly/perch_csv_data
- read_csv() 함수로 데이터프레임을 만든 다음 to_numpy() 메서드를 사용해 넘파이 배열로 바꾼다.


```python
import pandas as pd   # pd는 관례적으로 사용하는 판다스의 별칭이다.
df = pd.read_csv('https://bit.ly/perch_csv_data')
perch_full = df.to_numpy()
print(perch_full)
```

    [[ 8.4   2.11  1.41]
     [13.7   3.53  2.  ]
     [15.    3.82  2.43]
     [16.2   4.59  2.63]
     [17.4   4.59  2.94]
     [18.    5.22  3.32]
     [18.7   5.2   3.12]
     [19.    5.64  3.05]
     [19.6   5.14  3.04]
     [20.    5.08  2.77]
     [21.    5.69  3.56]
     [21.    5.92  3.31]
     [21.    5.69  3.67]
     [21.3   6.38  3.53]
     [22.    6.11  3.41]
     [22.    5.64  3.52]
     [22.    6.11  3.52]
     [22.    5.88  3.52]
     [22.    5.52  4.  ]
     [22.5   5.86  3.62]
     [22.5   6.79  3.62]
     [22.7   5.95  3.63]
     [23.    5.22  3.63]
     [23.5   6.28  3.72]
     [24.    7.29  3.72]
     [24.    6.38  3.82]
     [24.6   6.73  4.17]
     [25.    6.44  3.68]
     [25.6   6.56  4.24]
     [26.5   7.17  4.14]
     [27.3   8.32  5.14]
     [27.5   7.17  4.34]
     [27.5   7.05  4.34]
     [27.5   7.28  4.57]
     [28.    7.82  4.2 ]
     [28.7   7.59  4.64]
     [30.    7.62  4.77]
     [32.8  10.03  6.02]
     [34.5  10.26  6.39]
     [35.   11.49  7.8 ]
     [36.5  10.88  6.86]
     [36.   10.61  6.74]
     [37.   10.84  6.26]
     [37.   10.57  6.37]
     [39.   11.14  7.49]
     [39.   11.14  6.  ]
     [39.   12.43  7.35]
     [40.   11.93  7.11]
     [40.   11.73  7.22]
     [40.   12.38  7.46]
     [40.   11.14  6.63]
     [42.   12.8   6.87]
     [43.   11.93  7.28]
     [43.   12.51  7.42]
     [43.5  12.6   8.14]
     [44.   12.49  7.6 ]]
    

- 타깃 데이터는 이전과 동일한 방식으로 준비한다.




```python
import numpy as np

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

- 그 다음 perch_full과 perch_weight를 훈련 세트와 테스트 세트로 나눈다.


```python
from sklearn.model_selection import train_test_split

train_input, test_input, train_target, test_target = train_test_split( 
    perch_full, perch_weight, random_state = 42
)

#train_input.shape, test_input.shape, train_target.shape, test_target.shape
```

- 이 데이터를 사용해 새로운 특성을 만든다.

### 사이킷런의 변환기
- 사이킷런은 특성을 만들거나 전처리하기 위한 다양한 클래스를 제공한다.
- 이런 클래스를 변환기(transformer)라고 부른다.
- 사이킷런의 모델 클래스에 일관된 fit(), score(), predict() 메서드가 있는 것처럼 변환기 클래스는 모두 fit(), transform()메서드를 제공한다

- 사용할 변환기는 PolynomialFeatures 클래스이다.
- 이 클래스는 sklearn.preprocessing패키지에 포함되어 있다.


```python
from sklearn.preprocessing import PolynomialFeatures
```

- 2개의 특성 2와 3으로 이루어진 샘플 하나를 적용해본다.
- 이 클래스의 객체를 만르고 fit(), transform() 메서드를 차례대로 호출한다.


```python
poly = PolynomialFeatures()
poly.fit([[2, 3]])
print(poly.transform([[2, 3]]))
```

    [[1. 2. 3. 4. 6. 9.]]
    

- fit()
  - 새롭게 만들 특성 조합을 찾는다.
- transform()
  - 실제로 데이터를 변환한다.

- 위 코드에서 fit()메서드에 입력데이터만 전달했다.
- 즉 여기에서는 2개의 특성을 가진 샘플 [2,3]이 6개의 특성을 가진 샘플 [1. 2. 3. 4. 6. 9.]로 바뀌었다.

- PolynomialFeatures 클래스는 기본적으로 각 특성을 제곱한 항을 추가하고 특성끼리 서로 곱한 항을 추가한다.
- 2와 3을 각각 제곱한 4와 9가 추가되었고, 2와 3을 곱한 6이 추가된다. 1은 다음 식에 의해 추가된다.
- 무게 = a x 길이 + b x 높이 + c x 두께 + d x 1


- 이렇게 놓고 보면 특성은 (길이, 높이, 두께, 1)이 된다.
- 하지만 사이킷런의 선형 모델은 자동으로 절편(계수)을 추가하므로 굳이 이렇게 특성을 만들 필요가 없다.
- include_bias = False로 지정하여 다시 특성을 변환한다.


```python
poly = PolynomialFeatures(include_bias=False)
poly.fit([[2, 3]])
print(poly.transform([[2, 3]]))
```

    [[2. 3. 4. 6. 9.]]
    

- 절편을 위한 항이 제거되고 특성의 제곱과 특성끼리 곱한 항만 추가되었다.
- 이제 이 방식으로 train_input에 적용한다.
- train_input을 변환한 데이터를 train_poly에 저장하고 이 배열의 크기를 확인해 보자.


```python
poly = PolynomialFeatures(include_bias=False)
poly.fit(train_input)
train_poly = poly.transform(train_input)
print(train_poly.shape)
```

    (42, 9)
    

- PolynomialFeaures 클래스는 9개의 특성이 어떻게 만들어졌는지 확인하는 아주 좋은 방법을 제공한다.
- get_feature-names_out() 메서드를 호출하면 9개의 특성이 각각 어떤 입력의 조합으로 만들어졌는지 알려준다.




```python
poly.get_feature_names_out()
```




    array(['x0', 'x1', 'x2', 'x0^2', 'x0 x1', 'x0 x2', 'x1^2', 'x1 x2',
           'x2^2'], dtype=object)



- x0은 첫 번째 특성을 의미하고 x0^2는 첫 번째 특성의 제곱, x0 x1은 첫 번째와 두 번째 특성의 곱을 타나내는 식이다.
- 이제 테스트 세트를 변환한다.


```python
test_poly = poly.transform(test_input)
```

- 이어서 변환된 특성을 사용하여 다중 회귀 모델을 훈련한다.

### 다중 회귀 모델 훈련하기
- 사이킷런의 LinearRegression 클래스를 임포트하고 앞에서 만든 train_poly를 사용해 모델을 훈련시킨다.


```python
from sklearn.linear_model import LinearRegression
lr = LinearRegression()
lr.fit(train_poly, train_target)
print(lr.score(train_poly, train_target))
```

    0.9903183436982124
    

- 높은 점수가 나왔다.
- 농어의 길이뿐만 아니라 높이와 두께를 모두 사용했고 각 특성을 제곱하거나 서로 곱해서 다항 특성을 더 추가했다.
- 특성이 늘어나면 선형 회귀의 능력이 강해짐을 알 수 있다.


```python
print(lr.score(test_poly, test_target))
```

    0.9714559911594134
    

- 테스트 셑트에 대한 점수는 높아지지 않았지만 농어의 길이만 사용했을 때 있던 과소적합 문제가 더 이상 나타나지 않게 되었다.
- 특성을 더 많이 추가하면 어떻게될까? 3제곱, 4제곱 항까지 넣는 것이다.
- PolynomialFeaures 클래스의 degree 매개변수를 사용하여 필요한 고차항의 최대 차수를 지정할 수 있다.
- 5제곱까지 특성을 만들어 출력해본다.


```python
poly = PolynomialFeatures(degree=5, include_bias=False)
poly.fit(train_input)
train_poly = poly.transform(train_input)
test_poly = poly.transform(test_input)
print(train_poly.shape)
```

    (42, 55)
    

- 만들어진 특성의 개수가 무려 55개나 된다.
- train_poly 배열의 열의 개수가 특성의 개수이다.
- 이 데이터를 사용해 선형 회귀 모델을 다시 훈련한다.


```python
lr.fit(train_poly, train_target)
print(lr.score(train_poly, train_target))
```

    0.9999999999991097
    

- 거의 완벽한 점수다.
- 테스트 세트에 대한 점수는 어떨까?


```python
print(lr.score(test_poly, test_target))
```

    -144.40579242684848
    

- 음수가 나왔다.
- 특성의 개수를 늘리면 선형 모델은 더 강력해진다.
- 하지만 이런 모델은 훈련 세트에 너무 과대적합되므로 테스트 세트에서는 형편없는 점수를 만든다.

- 이 문제를 해결하기 위해 2가지 방법이 있다.
  - 방법 1. 다시 특성을 줄인다.
  - 방법 2. 규제를 사용한다.

### 규제 (regularization)
- 규제는 머신러닝 모델이 훈련 세트를 너무 과도하게 학습하지 못하도록 훼방하는 것을 말한다.
- 즉 모델이 훈련 세트에 과대적합되지 않도록 만드는 것이다.
- 회귀 모델의 경우 특성에 곱해지는 계수(또는 기울기)의 크기를 작게 만드는 일이다.



```python
# 규제하기 전에 먼저 정규화를 진행한다.
from sklearn.preprocessing import StandardScaler  # 이 클래스는 변환기의 하나이다.
ss = StandardScaler()
ss.fit(train_poly)
train_scaled = ss.transform(train_poly)
test_scaled = ss.transform(test_poly)
```

- StandardScaler 클래스의 객체 ss를 초기화한 후 PolynomialFeatures 클래스로 만든 train_poly를 사용해 이 객체를 훈련한다.
- 반드시 훈련 세트로 학습한 변환기를 사용해 테스트 세트까지 변환해야 한다.
- 이제 표준점수로 변환한 train_scaled와 test_scaled가 준비되었다.

### 릿지(ridge)와 라쏘(lasso)
- 선형 회귀 모델에 규제를 추가한 모델이다.
- 두 모델은 규제를 가하는 방법이 다르다.
- 릿지 
  - 계수를 제곱한 값을 기준으로 규제를 적용한다.
- 라쏘
  - 계수의 절댓값을 기준으로 규제를 적용한다.

### 릿지 회귀
- 릿지와 라쏘 모두 sklearn.linear_model 패키지 안에 있다.
- 모델 객체를 만들고 fit() 메서드에서 훈련한 다음 score()메서드로 평가한다.
- 앞서 준비한 train_scaled 데이터로 릿지 모델을 훈련한다.


```python
from sklearn.linear_model import Ridge
ridge = Ridge()
ridge.fit(train_scaled, train_target)
print(ridge.score(train_scaled, train_target))
```

    0.9896101671037343
    

- 선형 회귀에 비해 낮아졌다.
- 이번에는 테스트 세트에 대한 점수를 확인한다.


```python
print(ridge.score(test_scaled, test_target))
```

    0.9790693977615397
    

- 확실히 과대적합도지 않아 테스트 세트에서도 좋은 성능을 내고 있다.
- 릿지와 라쏘 모델을 사용할 때 규제의 양을 임의로 조절할 수 있다.
- 모델 객체를 만들 때 alpha매개변수로 규제의 강도를 조절한다.
- alpha 값이 크면 규제 강도가 세지므로 계수 값을 줄이고 더 과소적합되도록 유도한다.
- aplha 값이 작으면 계수를 줄이는 역할이 줄어들고 선형 회귀 모델과 유사해지므로 과대적합될 가능성이 크다.

- 적절한 alpha값을 찾는 한 가지 방법은 alpha값에 R^2값의 그래프를 그려 보는 것이다.
- 훈련 세트와 테스트 세트의 점수가 가장 가까운 지점이 최적의 alpha 값이 된다.
- alpha값을 바꿀 때마다 score() 메서드의 결과를 저장할 리스트를 만든다.


```python
import matplotlib.pyplot as plt
train_score = []
test_score = []
```

- 다음은 alpha를 0.001에서 100까지 10배씩 늘려가며 릿지 회귀 모델을 훈련한 다음 훈련 세트와 테스트 세트의 점수를 리스트에 저장한다.

- 사람이 직버 지정해야 하는 매개변수 (하이퍼 파라미터)
- 다 돌려봐서 성능이 놓은 alpha 값 찾기
- 경우의 수 (15가지)
  + A 조건 : 5가지
  + B 조건 : 3가지 


```python
alpha_list = [0.001, 0.01, 0.1, 1, 10, 100]
for alpha in alpha_list:
  # 릿지 모델을 만든다.
  ridge = Ridge(alpha=alpha)
  # 릿지 모델을 훈련한다.
  ridge.fit(train_scaled, train_target)
  # 훈련 점수와 테스트 점수를 저장한다.
  train_score.append(ridge.score(train_scaled, train_target))
  test_score.append(ridge.score(test_scaled, test_target))
```

- 이제 그래프를 그려본다.
- alpha 값을 10배씩 늘렸기 때문에 그래프 일부가 너무 촘촘해진다.
- alpha_list에 있는 6개의 값을 동일한 간격으로 나타내기 위해 로그 함수로 바꾸어 지수로 표현한다.
  - 0.001은 -3, 0.01은 -2가 되는 식이다. 


```python
plt.plot(np.log10(alpha_list), train_score)
plt.plot(np.log10(alpha_list), test_score)
plt.xlabel('alpha')
plt.ylabel('R^2')
plt.show()
```


    
![png](/images/chapter3_3_김민균/output_57_0.png)
    


- 위는 훈련 세트 그래프, 아래는 테스트 세트 그래프이다.
- 이 그래프 왼쪽에서 두 세트의 점수 차이가 크다.
- 훈련 세트에만 잘 맞는 과대적합의 전형적인 모습니다.
- 반대로 오른쪽에서는 두 세트의 점수가 모두 낮아지는 과소적합이 나타난다.

- 적절한 alpha값은 두 그래프가 가장 가깝고 테스트 세트의 점수가 가장 높은 -1, 즉 10^-1 = 0.1 이다.
- alpha 값을 0.1로 하여 최종 모델을 훈련한다.


```python
ridge = Ridge(alpha=0.1)
ridge.fit(train_scaled, train_target)
print(ridge.score(train_scaled, train_target))
print(ridge.score(test_scaled, test_target))
```

    0.9903815817570366
    0.9827976465386926
    

- 이 모델은 훈련 세트와 테스트 세트의 점수가 비슷하게 모두 높고 과대적합과 과소적합 사이에서 균형을 맞추고 있다.
- 이번에는 라쏘 모델을 훈련해보자.

### 라쏘 회귀
- 라쏘 모델을 훈련하는 것은 릿지와 매우 비슷하다.
- Ridge 클래스를 Lasso 클래스로 바꾸는 것이 전부이다.


```python
from sklearn.linear_model import Lasso
lasso = Lasso()
lasso.fit(train_scaled, train_target)
print(lasso.score(train_scaled, train_target))
```

    0.989789897208096
    

- 라소도 과대적합을 잘 억제한 결과를 보여준다.
- 테스트 세트의 점수도 확인한다.


```python
print(lasso.score(test_scaled, test_target))
```

    0.9800593698421883
    

- 릿지만큼 좋은 점수가 나왔다.
- 앞에서와 같이 alpha값을 바꾸어 가며 훈련 세트와 테스트 세트에 대한 점수를 계산한다.


```python
train_score = []
test_score = []
alpha_list = [0.001, 0.01, 0.1, 1, 10, 100]
for alpha in alpha_list:
  # 라쏘 모델을 만든다.
  lasso = Lasso(alpha=alpha, max_iter = 10000)  # 반복 횟수를 충분히 늘리기 위해 값을 지정.
  # 라쏘 모델을 훈련한다.
  lasso.fit(train_scaled, train_target)
  # 훈련 점수와 테스트 점수를 저장한다.
  train_score.append(lasso.score(train_scaled, train_target))
  test_score.append(lasso.score(test_scaled, test_target))
```

    /usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_coordinate_descent.py:648: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations, check the scale of the features or consider increasing regularisation. Duality gap: 1.878e+04, tolerance: 5.183e+02
      coef_, l1_reg, l2_reg, X, y, max_iter, tol, rng, random, positive
    /usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_coordinate_descent.py:648: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations, check the scale of the features or consider increasing regularisation. Duality gap: 1.297e+04, tolerance: 5.183e+02
      coef_, l1_reg, l2_reg, X, y, max_iter, tol, rng, random, positive
    

- train_score와 test_score 리스트를 사용해 그래프를 그린다.
- 이 그래프도 x축은 로그 스케일로 바꿔 그린다.


```python
plt.plot(np.log10(alpha_list), train_score)
plt.plot(np.log10(alpha_list), test_score)
plt.xlabel('alpha')
plt.ylabel('R^2')
plt.show()
```


    
![png](/images/chapter3_3_김민균/output_69_0.png)
    


- 이 그래프도 왼쪽은 과대적합을 부여주고 있고, 오른쪽으로 갈수록 두 세트의 점수가 좁혀지고 있다.
- 라쏘 모델에서 최적의 alpha값은 1, 즉 10^1 = 10이다.
  - 이 값으로 다시 모델을 훈련한다.


```python
lasso = Lasso(alpha=0.1)
lasso.fit(train_scaled, train_target)
print(lasso.score(train_scaled, train_target))
print(lasso.score(test_scaled, test_target))
```

    0.990137631128448
    0.9819405116249363
    

    /usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_coordinate_descent.py:648: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations, check the scale of the features or consider increasing regularisation. Duality gap: 8.062e+02, tolerance: 5.183e+02
      coef_, l1_reg, l2_reg, X, y, max_iter, tol, rng, random, positive
    

- 모델이 잘 훈련되었다.
- 라쏘 모델은 계수 값을 아예 0으로 만들 수 있다.
- 라쏘 모델의 계수는 coef_ 속성에 저장되어 있다. 이 중에 0인 것을 헤아려본다.


```python
print(np.sum(lasso.coef_ == 0))
```

    35
    

- 많은 계수가 0이 되었다.
- 55개의 특성을 모델에 주입했지만 라소 모델이사용한 특성은 15개 밖에 되지 않는다.
- 이런 특징 때문에 라쏘 모델을 유용한 특성을 골라내는 용도로도 사용할 수 있다.

### 전체 소스 코드
- 다음 주소를 참고하라 : https://bit.ly/hg-03-3


```python
# 특성 공학과 규제

# 데이터 준비
import pandas as pd

df = pd.read_csv('https://bit.ly/perch_csv_data')
perch_full = df.to_numpy()
print(perch_full)

import numpy as np

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

train_input, test_input, train_target, test_target = train_test_split(perch_full, perch_weight, random_state=42)

# 사이킷런의 변환기

from sklearn.preprocessing import PolynomialFeatures

poly = PolynomialFeatures()
poly.fit([[2, 3]])
print(poly.transform([[2, 3]]))

poly = PolynomialFeatures(include_bias=False)
poly.fit([[2, 3]])
print(poly.transform([[2, 3]]))

poly = PolynomialFeatures(include_bias=False)
poly.fit(train_input)
train_poly = poly.transform(train_input)
print(train_poly.shape)

poly.get_feature_names_out()

test_poly = poly.transform(test_input)

# 다중 회귀 모델 훈련하기
from sklearn.linear_model import LinearRegression

lr = LinearRegression()
lr.fit(train_poly, train_target)
print(lr.score(train_poly, train_target))

print(lr.score(test_poly, test_target))

poly = PolynomialFeatures(degree=5, include_bias=False)
poly.fit(train_input)
train_poly = poly.transform(train_input)
test_poly = poly.transform(test_input)
print(train_poly.shape)

lr.fit(train_poly, train_target)
print(lr.score(train_poly, train_target))

print(lr.score(test_poly, test_target))

# 규제

from sklearn.preprocessing import StandardScaler

ss = StandardScaler()
ss.fit(train_poly)
train_scaled = ss.transform(train_poly)
test_scaled = ss.transform(test_poly)

# 릿지 회귀
from sklearn.linear_model import Ridge

ridge = Ridge()
ridge.fit(train_scaled, train_target)
print(ridge.score(train_scaled, train_target))

print(ridge.score(test_scaled, test_target))

import matplotlib.pyplot as plt

train_score = []
test_score = []

alpha_list = [0.001, 0.01, 0.1, 1, 10, 100]
for alpha in alpha_list:
    # 릿지 모델을 만듭니다
    ridge = Ridge(alpha=alpha)
    # 릿지 모델을 훈련합니다
    ridge.fit(train_scaled, train_target)
    # 훈련 점수와 테스트 점수를 저장합니다
    train_score.append(ridge.score(train_scaled, train_target))
    test_score.append(ridge.score(test_scaled, test_target))

plt.plot(np.log10(alpha_list), train_score)
plt.plot(np.log10(alpha_list), test_score)
plt.xlabel('alpha')
plt.ylabel('R^2')
plt.show()

ridge = Ridge(alpha=0.1)
ridge.fit(train_scaled, train_target)

print(ridge.score(train_scaled, train_target))
print(ridge.score(test_scaled, test_target))

from sklearn.linear_model import Lasso

lasso = Lasso()
lasso.fit(train_scaled, train_target)
print(lasso.score(train_scaled, train_target))

print(lasso.score(test_scaled, test_target))

train_score = []
test_score = []

alpha_list = [0.001, 0.01, 0.1, 1, 10, 100]
for alpha in alpha_list:
    # 라쏘 모델을 만듭니다
    lasso = Lasso(alpha=alpha, max_iter=10000)
    # 라쏘 모델을 훈련합니다
    lasso.fit(train_scaled, train_target)
    # 훈련 점수와 테스트 점수를 저장합니다
    train_score.append(lasso.score(train_scaled, train_target))
    test_score.append(lasso.score(test_scaled, test_target))

plt.plot(np.log10(alpha_list), train_score)
plt.plot(np.log10(alpha_list), test_score)
plt.xlabel('alpha')
plt.ylabel('R^2')
plt.show()

lasso = Lasso(alpha=10)
lasso.fit(train_scaled, train_target)

print(lasso.score(train_scaled, train_target))
print(lasso.score(test_scaled, test_target))

print(np.sum(lasso.coef_ == 0))
```

    [[ 8.4   2.11  1.41]
     [13.7   3.53  2.  ]
     [15.    3.82  2.43]
     [16.2   4.59  2.63]
     [17.4   4.59  2.94]
     [18.    5.22  3.32]
     [18.7   5.2   3.12]
     [19.    5.64  3.05]
     [19.6   5.14  3.04]
     [20.    5.08  2.77]
     [21.    5.69  3.56]
     [21.    5.92  3.31]
     [21.    5.69  3.67]
     [21.3   6.38  3.53]
     [22.    6.11  3.41]
     [22.    5.64  3.52]
     [22.    6.11  3.52]
     [22.    5.88  3.52]
     [22.    5.52  4.  ]
     [22.5   5.86  3.62]
     [22.5   6.79  3.62]
     [22.7   5.95  3.63]
     [23.    5.22  3.63]
     [23.5   6.28  3.72]
     [24.    7.29  3.72]
     [24.    6.38  3.82]
     [24.6   6.73  4.17]
     [25.    6.44  3.68]
     [25.6   6.56  4.24]
     [26.5   7.17  4.14]
     [27.3   8.32  5.14]
     [27.5   7.17  4.34]
     [27.5   7.05  4.34]
     [27.5   7.28  4.57]
     [28.    7.82  4.2 ]
     [28.7   7.59  4.64]
     [30.    7.62  4.77]
     [32.8  10.03  6.02]
     [34.5  10.26  6.39]
     [35.   11.49  7.8 ]
     [36.5  10.88  6.86]
     [36.   10.61  6.74]
     [37.   10.84  6.26]
     [37.   10.57  6.37]
     [39.   11.14  7.49]
     [39.   11.14  6.  ]
     [39.   12.43  7.35]
     [40.   11.93  7.11]
     [40.   11.73  7.22]
     [40.   12.38  7.46]
     [40.   11.14  6.63]
     [42.   12.8   6.87]
     [43.   11.93  7.28]
     [43.   12.51  7.42]
     [43.5  12.6   8.14]
     [44.   12.49  7.6 ]]
    [[1. 2. 3. 4. 6. 9.]]
    [[2. 3. 4. 6. 9.]]
    (42, 9)
    0.9903183436982124
    0.9714559911594134
    (42, 55)
    0.9999999999991097
    -144.40579242684848
    0.9896101671037343
    0.9790693977615397
    


    
![png](/images/chapter3_3_김민균/output_76_1.png)
    


    0.9903815817570366
    0.9827976465386926
    0.989789897208096
    0.9800593698421883
    

    /usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_coordinate_descent.py:648: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations, check the scale of the features or consider increasing regularisation. Duality gap: 1.878e+04, tolerance: 5.183e+02
      coef_, l1_reg, l2_reg, X, y, max_iter, tol, rng, random, positive
    /usr/local/lib/python3.7/dist-packages/sklearn/linear_model/_coordinate_descent.py:648: ConvergenceWarning: Objective did not converge. You might want to increase the number of iterations, check the scale of the features or consider increasing regularisation. Duality gap: 1.297e+04, tolerance: 5.183e+02
      coef_, l1_reg, l2_reg, X, y, max_iter, tol, rng, random, positive
    


    
![png](/images/chapter3_3_김민균/output_76_4.png)
    


    0.9888067471131867
    0.9824470598706695
    40
    

- Reference : 혼자 공부하는 머신러닝 + 딥러닝
