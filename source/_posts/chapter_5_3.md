---
title: "chapter_5_3"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 알고리즘
author: "minkuen"
date: '2022-04-05'
---

# 트리의 앙상블
- lightGBM 기억!
  + GBM --> XGBoost --> LightGBM
  + 참고 1. 모델개발속도가 빨라졌나?
  + 참고 2. 모델의 성능이 좋아졌나?
- TabNet(2019)
  + 딥러닝 컨셉!

### 랜덤 포레스트(Forest)
- 결정 트리를 랜덤하게 만들어 결정 트리의 숲을 만든다.
- 결정 트리 나무를 500개 심기
- 최종적인 결정은 투표 방식
  + 나무-1 : 양성
  + 나무_2 : 음성
  + 나무_3 : 양성
  ..
  + 나무-500 : 양성


- 데이터 불러오기
- 넘파이 배열로 변환
- 데이터 세트 나누기


```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split

wine = pd.read_csv('https://bit.ly/wine_csv_data')

data = wine[['alcohol', 'sugar', 'pH']].to_numpy()
target = wine['class'].to_numpy()

train_input, test_input, train_target, test_target = train_test_split(data, 
                                                                      target, 
                                                                      test_size=0.2, 
                                                                      random_state=42)
```

- 267p
  + cross_validate()함수 : 교차 검증 수행 
  + RandomForestClassifier는 기본적으로 100개의 트리를 사용하므로 n_jops=-1로 지정하여 모든 CPU 코어를 사용한다.


```python
from sklearn.model_selection import cross_validate
from sklearn.ensemble import RandomForestClassifier
rf = RandomForestClassifier(n_jobs=-1, random_state=42)   # n_jobs = -1은 pc의 모든 코어를 사용하겠다는 뜻
scores = cross_validate(rf, train_input, train_target,
                        return_train_score = True, n_jobs=-1)

print(np.mean(scores['train_score']), np.mean(scores['test_score']))
```

    0.9973541965122431 0.8905151032797809
    

- 랜덤 포레스트는 결정 트리의 앙상블이기 때문에 DecisionTreeClassifier가 제공하는 매개변수를 모두 제공한다.
- 또한 결정 트리의 큰 장점 중 하나인 특성 중요도를 계산한다.
- 랜덤 포레스트 모델을 훈련 세트에 훈련한 후 특성 중요도를 출력해 본다.


```python
rf.fit(train_input, train_target)
print(rf.feature_importances_)
```

    [0.23167441 0.50039841 0.26792718]
    

- 두 번째 특성인 sugar가 가장 중요도가 높다는 것을 알 수 있다.

- RandomForestClassifier는 자체적으로 모델을 평가하는 점수를 얻을 수도 있다.
- 이 점수를 얻으려면 RandomForestClassifier 클래스의 oob_score 매개변수를 True로 지정해야 한다.
- oob_score = True로 지정하고 모델을 훈련하여 OOB 점수를 출력해보자.


```python
rf = RandomForestClassifier(oob_score = True, n_jobs=-1, random_state=42)
rf.fit(train_input, train_target)
print(rf.oob_score_)
```

    0.8934000384837406
    

- 교차 검즈에서 얻은 점수와 매우 비슷한 결과를 얻었다.

### 그래이디언트 부스팅
- 그 이전 트리의 오차를 보완하는 방식으로 사용
- 깊이가 얕은 트리를 사용.
- 학습률 매개변수로 속도를 조절.
- 단점 : 속도가 느림.


```python
from sklearn.ensemble import GradientBoostingClassifier
gb = GradientBoostingClassifier(random_state=42)
scores = cross_validate(gb, train_input, train_target,
                        return_train_score = True, n_jobs=-1)

print(np.mean(scores['train_score']), np.mean(scores['test_score']))
```

    0.8881086892152563 0.8720430147331015
    

- 거의 과대적합이 되지 않았다.
- 그래디언트 부스팅은 결정 트리의 개수를 늘려도 과대적합에 매우 강하다.
- 학습률을 증가시키고 트리의 개수를 늘리면 조금 더 성능이 향상될 수 있다.


```python
gb = GradientBoostingClassifier(n_estimators = 500, learning_rate = 0.2, random_state = 42)
scores = cross_validate(gb, train_input, train_target,
                        return_train_score = True, n_jobs=-1)

print(np.mean(scores['train_score']), np.mean(scores['test_score']))
```

    0.9464595437171814 0.8780082549788999
    

- 결정 트리 개수를 500개로 늘렸다. 5배로 늘렸지만 과대적합을 잘 억제하고 있다.
- 학습률 learning_rate의 기본값은 0.1이다.
- 그레이디언트 부스팅도 특성 중요도를 제공한다.
- 결과에서 볼 수 있듯이 그레이디언트 부스팅이 랜덤 포레스트보다 일부 특성(당도)에 더 집중한다.


```python
gb.fit(train_input, train_target)
print(gb.feature_importances_)
```

    [0.15872278 0.68010884 0.16116839]
    

- 흐름
  + 0. 데이터 전처리 / 시각화
  + 1. 기본 모형으로 전체 흐름을 설계
  + 2. 여러 모형으로 비교 대조
  + 3. 교차 검증, 하이퍼 파라미터 성능 비교
  + ...
  + 1등 하는 그날까지

- Reference : 혼자 공부하는 머신러닝 + 딥러닝 
