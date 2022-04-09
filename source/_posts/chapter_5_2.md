---
title: "chapter_5_2"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 알고리즘
author: "minkuen"
date: '2022-04-04'
---
  
# 교차 검증과 그리드 서치
- 키워드 : 하이퍼 파라미터
- 데이터가 작을 때, 주로 사용
- 하이퍼 파라미터
  + max_depth : 3, 정확도가 84%
- 결론
  + 모르면 디폴트만 쓰자!
  + 가성비 (시간 대비 성능 보장 안됨!)


### 검증 세트
- 테스트 세트(1회성)
- 훈련 데이터를 훈련 데이터 + 검증 데이터로 재 분할

### 현실
- 테스트 데이터가 별도로 존재하지 않음!
- 전체 데이터 = 훈련 (6) : 검증 (2) : 테스트 (2)
  + 테스트 데이터는 모르는 데이터로 생각!

- 캐글
  - 캐글에서는 훈련, 테스트 데이터가 제공된다. 훈련 데이터만 한 번 쪼개서 사용하면 된다.

### 참고
- 사이킷 런 : https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html
- 구글링 : 그리드 탐색(서치) vs 랜덤 탐색(서치)


```python
import pandas as pd
wine = pd.read_csv("https://bit.ly/wine_csv_data")

data = wine[['alcohol', 'sugar', 'pH']].to_numpy()
target = wine['class'].to_numpy()
```


```python
from sklearn.model_selection import train_test_split

train_input, test_input, train_target, test_target = train_test_split(
    data, target, test_size=0.2, random_state=42
)
```


```python
sub_input, val_input, sub_target, val_target = train_test_split(
    train_input, train_target, test_size=0.2, random_state=42
)
```

### 모델 만든 후 평가


```python
from sklearn.tree import DecisionTreeClassifier
dt = DecisionTreeClassifier(random_state=42)
dt.fit(sub_input, sub_target)
print(dt.score(sub_input, sub_target))
print(dt.score(val_input, val_target))
```

    0.9971133028626413
    0.864423076923077
    

### 교차 검증
- 많이 하면 많이 할수록 좋다.
- 교차 검증의 목적 : 좋은 모델이 만들어진다!
  + 좋은 모델 != 성능 좋은 모델
  + 좋은 모델 = 과대 적합이 아닌 모델 = 모형의 오차가 적은 모델 = 안정적인 모델
- 교재 245p
  + 모델 평가 1 : 90%
  + 모델 평가 2 : 85%
  + 모델 평가 3 : 80%
- 단점 : 시간이 오래 걸림

### 교차 검증 함수


```python
from sklearn.model_selection import cross_validate
scores = cross_validate(dt, train_input, train_target)
print(scores)
```

    {'fit_time': array([0.01164412, 0.00772762, 0.00744891, 0.00796771, 0.00716805]), 'score_time': array([0.00128865, 0.00070405, 0.0007143 , 0.00097823, 0.00069904]), 'test_score': array([0.86923077, 0.84615385, 0.87680462, 0.84889317, 0.83541867])}
    

- 최종점수 평균 구하기


```python
import numpy as np
print(np.mean(scores['test_score']))
```

    0.855300214703487
    

- 훈련 세트 섞은 후, 10-폴드 교차검증


```python
from sklearn.model_selection import StratifiedKFold
splitter = StratifiedKFold(n_splits = 10, shuffle = True, random_state=42)
scores = cross_validate(dt, train_input, train_target, cv = splitter)

print(np.mean(scores['test_score']))
```

    0.8574181117533719
    

### 하이퍼 파라미터 튜닝 꼭 하고 싶다!
- 랜덤 서치 사용하자! 
  - 그리드 서치보다 편리하다
- 자동으로 잡아주는 라이브러리들이 등장하기 시작함
  - hyperopt


```python
%%time

from sklearn.model_selection import GridSearchCV
params = {
    'min_impurity_decrease' : [0.0001, 0.0002, 0.0003, 0.0004, 0.0005],
}
# dt = DecisionTreeClassifier(random_state=42)
gs = GridSearchCV(DecisionTreeClassifier(random_state=42), params, n_jobs=-1)
gs.fit(train_input, train_target)
```

    CPU times: user 83.8 ms, sys: 1.66 ms, total: 85.5 ms
    Wall time: 264 ms
    

- pamas에 2줄을 쓰면 시간이 2배 이상 더 걸린다.


```python
%%time

from sklearn.model_selection import GridSearchCV
params = {
    'min_impurity_decrease' : [0.0001, 0.0002, 0.0003, 0.0004, 0.0005],
    'max_depth' : [3, 4, 5, 6, 7]
}
# dt = DecisionTreeClassifier(random_state=42)
gs = GridSearchCV(DecisionTreeClassifier(random_state=42), params, n_jobs=-1)
gs.fit(train_input, train_target)
```

    CPU times: user 191 ms, sys: 1.13 ms, total: 192 ms
    Wall time: 674 ms
    


```python
%%time

from sklearn.model_selection import GridSearchCV
params = {
    'min_impurity_decrease' : [0.0001, 0.0002, 0.0003, 0.0004, 0.0005],
    'max_depth' : [3, 4, 5, 6, 7]
}
# dt = DecisionTreeClassifier(random_state=42)
gs = GridSearchCV(DecisionTreeClassifier(random_state=42), params, n_jobs=-1)
gs.fit(train_input, train_target)

dt = gs.best_estimator_
print(dt)
print(dt.score(train_input, train_target))
print(gs.best_params_)
```

    DecisionTreeClassifier(max_depth=7, min_impurity_decrease=0.0005,
                           random_state=42)
    0.8830094285164518
    {'max_depth': 7, 'min_impurity_decrease': 0.0005}
    CPU times: user 284 ms, sys: 38.7 ms, total: 323 ms
    Wall time: 2.15 s
    

- 이 부분에 의해 결과가 (5x5=)25개 출력된다.
  - 'min_impurity_decrease' : [0.0001, 0.0002, 0.0003, 0.0004, 0.0005]
  - 'max_depth' : [3, 4, 5, 6, 7]


```python
print(gs.cv_results_['mean_test_score'])
```

    [0.84125583 0.84125583 0.84125583 0.84125583 0.84125583 0.85337806
     0.85337806 0.85337806 0.85337806 0.85318557 0.85780355 0.85799604
     0.85857352 0.85857352 0.85838102 0.85645721 0.85799678 0.85876675
     0.85972866 0.86088306 0.85607093 0.85761031 0.85799511 0.85991893
     0.86280466]
    

### 랜덤 서치
- p252. 매개변수 값의목록을 전달하는 것이 아니라 매개변수를 샘플링할 수 있도록 확률 분포 객체를 전달.


```python
from scipy.stats import uniform, randint
rgen = randint(0, 10)
rgen.rvs(10)
```




    array([7, 9, 7, 4, 2, 0, 4, 8, 6, 3])




```python
np.unique(rgen.rvs(1000), return_counts = True)
```




    (array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]),
     array([103,  90,  88, 110,  84, 115, 105, 102, 104,  99]))



- 254p


```python
from sklearn.model_selection import RandomizedSearchCV

params = {
    'min_impurity_decrease' : uniform(0.0001, 0.001),
    'max_depth' : randint(20,50)
}

gs = RandomizedSearchCV(DecisionTreeClassifier(random_state=42),
                        params, n_iter = 100, n_jobs = -1, random_state=42)

gs.fit(train_input, train_target)
```




    RandomizedSearchCV(estimator=DecisionTreeClassifier(random_state=42),
                       n_iter=100, n_jobs=-1,
                       param_distributions={'max_depth': <scipy.stats._distn_infrastructure.rv_frozen object at 0x7fa6910bdd90>,
                                            'min_impurity_decrease': <scipy.stats._distn_infrastructure.rv_frozen object at 0x7fa6907f3810>},
                       random_state=42)



- 위 parmas에 정의된 매개변수 범위에서 총 100번(n_iter 매개변수)을 샘플링하여 교차 검증을 수행하고 최적의 매개변수 조합을 찾는다.
- 앞서 그리드 서치보다 훨씬 교차 검증 수를 줄이면서 넓은 영역을 효과적으로 탐색할 수 있다.
- 결과를 확인해보자. 먼저 최적의 매개변수 조합을 출력한다.


```python
print(gs.best_params_)
```

    {'max_depth': 29, 'min_impurity_decrease': 0.000437615171403628}
    

- 최고의 교차 검증 점수도 확인한다.


```python
print(np.max(gs.cv_results_['mean_test_score']))
```

    0.8689635004071962
    

- 최적의 모델은 이미 전체 훈련 세트(train_input, train_target)로 훈련되어 best_estimator_속성에 저장되어 있다. 
- 이 모델을 최종 모델로 결정하고 테스트 세트의 성능을 확인해 보자


```python
dt = gs.best_estimator_
print(dt.score(test_input, test_target))
```

    0.8638461538461538
    

- 테스트 세트 점수는 검증 세트에 대한 점수보다 조금 작은 것이 일반적이다.
- 여기까지 두 서치를 사용해 본 결과, 랜덤 서치가 더 사용하기 용이하였다.

- Reference : 혼자 공부하는 머신러닝 + 딥러닝
