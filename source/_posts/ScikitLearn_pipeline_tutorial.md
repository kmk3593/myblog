---
title: "Scikitlearn_pipeline_tutorial"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 인공신경망
author: "minkuen"
date: '2022-04-09'
---

# 데이터 누수 방지 위한 모델링 기법 : 파이프라인 구축
- 수능 시험 = 최종 테스트 데이터
- 모의고사 또는 과거 기출문제 = 검증데이터
- 교과서 문제지 = 훈련 데이터
- 머신러닝 엔지니어 : MLOps (선행되어야 하는 코드 조건, Pipeline 형태로 구축)
  + 머신러닝 코드 자동화 가능! 운영 가능!
  + 개발업계의 최상위 연봉자!

### 데이터 불러오기


```python
import pandas as pd
import numpy as np
data = pd.read_csv('https://raw.githubusercontent.com/MicrosoftDocs/ml-basics/master/data/daily-bike-share.csv')
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 731 entries, 0 to 730
    Data columns (total 14 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   instant     731 non-null    int64  
     1   dteday      731 non-null    object 
     2   season      731 non-null    int64  
     3   yr          731 non-null    int64  
     4   mnth        731 non-null    int64  
     5   holiday     731 non-null    int64  
     6   weekday     731 non-null    int64  
     7   workingday  731 non-null    int64  
     8   weathersit  731 non-null    int64  
     9   temp        731 non-null    float64
     10  atemp       731 non-null    float64
     11  hum         731 non-null    float64
     12  windspeed   731 non-null    float64
     13  rentals     731 non-null    int64  
    dtypes: float64(4), int64(9), object(1)
    memory usage: 80.1+ KB
    

### 데이터 추출


```python
cols = ['season', 'mnth', 'holiday', 'weekday', 'workingday', 'weathersit', 'temp', 'atemp', 'hum', 'windspeed', 'rentals']
data = data[cols]
data.info()
# data['mnth'].value_counts()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 731 entries, 0 to 730
    Data columns (total 11 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   season      731 non-null    int64  
     1   mnth        731 non-null    int64  
     2   holiday     731 non-null    int64  
     3   weekday     731 non-null    int64  
     4   workingday  731 non-null    int64  
     5   weathersit  731 non-null    int64  
     6   temp        731 non-null    float64
     7   atemp       731 non-null    float64
     8   hum         731 non-null    float64
     9   windspeed   731 non-null    float64
     10  rentals     731 non-null    int64  
    dtypes: float64(4), int64(7)
    memory usage: 62.9 KB
    

- Data Preprocessing
  + 결측치 수동으로 채우거나
  + 불필요한 변수를 제거하거나
  + 이상치를 제거하거나
  + 파생변수를 만들거나 등

기본 : 데이터 불러오기 -> 데이터 전처리 -> 피처공학(원핫-인코딩) -> 데이터셋 분리 -> 모델링 코드 -> 모델평가

파이프라인 : 데이터 불러오기  -> 데이터 전처리 -> 데이터셋 분리 -> 파이프라인 구축(피처공학, 모델링 코드) -> 모델 평가

### 데이터 셋 분리


```python
from sklearn.model_selection import train_test_split
X = data.drop('rentals',axis=1)
y = data['rentals']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=123)
```

- Feature Engineering
  - 기존 : 개별적으로 코드 작성
  - 현재 : Pipeline 코드로 추가할 것

### Pipeline 구축


```python
from sklearn.preprocessing import StandardScaler, OrdinalEncoder, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline

# 데이터 타입 3가지
# 수치형 데이터, 문자열 데이터
# 문자열 데이터 : 범주형(명목형, 서열형 데이터로 구분됨)
numeric_transformer = Pipeline(steps=[
       ('imputer', SimpleImputer(strategy='mean'))
      ,('scaler', StandardScaler())
])

ordinal_transformer = Pipeline(steps=[
       ('imputer', SimpleImputer(strategy='constant'))
      ,('ordEncoder', OrdinalEncoder())
])

onehot_transformer = Pipeline(steps=[
       ('imputer', SimpleImputer(strategy='constant'))
      ,('oheEncoder', OneHotEncoder())                                   
])

# 수치형 데이터 및 Categorical 데이터 컬럼 분리

numeric_features = ['temp', 'atemp', 'hum', 'windspeed']
ordinal_features = ['holiday', 'weekday', 'workingday', 'weathersit']
onehot_features  = ['season', 'mnth']

# numeric_features = data.select_dtypes(include=['int64', 'float64']).columns
# categorical_features = data.select_dtypes(include=['object']).drop(['Loan_Status'], axis=1).columns

preprocessor = ColumnTransformer(
   transformers=[
     ('numeric', numeric_transformer, numeric_features)
   , ('ord_categorical', ordinal_transformer, ordinal_features)
   , ('ohe_categorical', onehot_transformer, onehot_features)
])
```

# 모델 적용
- 전처리가 끝났으니 모델을 적용한다.


```python
from sklearn.ensemble import RandomForestRegressor

pipeline = Pipeline(steps = [
               ('preprocessor', preprocessor)
              ,('regressor', RandomForestRegressor())
           ])

rf_model = pipeline.fit(X_train, y_train)
print(rf_model)
```

    Pipeline(steps=[('preprocessor',
                     ColumnTransformer(transformers=[('numeric',
                                                      Pipeline(steps=[('imputer',
                                                                       SimpleImputer()),
                                                                      ('scaler',
                                                                       StandardScaler())]),
                                                      ['temp', 'atemp', 'hum',
                                                       'windspeed']),
                                                     ('ord_categorical',
                                                      Pipeline(steps=[('imputer',
                                                                       SimpleImputer(strategy='constant')),
                                                                      ('ordEncoder',
                                                                       OrdinalEncoder())]),
                                                      ['holiday', 'weekday',
                                                       'workingday',
                                                       'weathersit']),
                                                     ('ohe_categorical',
                                                      Pipeline(steps=[('imputer',
                                                                       SimpleImputer(strategy='constant')),
                                                                      ('oheEncoder',
                                                                       OneHotEncoder())]),
                                                      ['season', 'mnth'])])),
                    ('regressor', RandomForestRegressor())])
    

- 파이프라인끼리 연결시켜서 길게 늘이는 원리
  - 데이터가 라인을 따라 흐르게 된다. 자동화

### 모델 평가


```python
from sklearn.metrics import r2_score
predictions = rf_model.predict(X_test)
print (r2_score(y_test, predictions))
```

    0.7728368422640097
    

### 다중 모형 개발


```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.tree import DecisionTreeRegressor

regressors = [
    RandomForestRegressor()
   ,DecisionTreeRegressor()
]

# regressors = [pipe_rf, pipe_dt]
for regressor in regressors:
    pipeline = Pipeline(steps = [
               ('preprocessor', preprocessor)
              ,('regressor',regressor)
           ])
    model = pipeline.fit(X_train, y_train)
    predictions = model.predict(X_test)
    print(regressor)
    print(f'Model r2 score:{r2_score(predictions, y_test)}')
```

    RandomForestRegressor()
    Model r2 score:0.74544998600902
    DecisionTreeRegressor()
    Model r2 score:0.6365934810580942
    
- Reference : 혼자 공부하는 머신러닝 + 딥러닝