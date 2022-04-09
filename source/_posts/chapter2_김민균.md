---
title: "chapter2"
tags:
  - python
  - machine learning
categories:
  - python
  - machine learning
  - 데이터 전처리
author: "minkuen"
date: '2022-03-28'
---


# 지도학습과 비지도 학습
- 지도학습 : 경진대외 유형
- 입력과 타깃 : 독립변수(입력), 종속변수(타깃)
- 정답이 있는 문제
  - 1 유형 : 타이타닉 생존자 분류 : survived (타깃)
  - 2 유형 : 카페 예상매출액 : 숫자를 예측
- 특성(Feature) : 독립변수(엑셀의 컬럼)

- 비지도 학습 : 뉴스기사 종류를 분류
  + 기사 1 : 사회, 의학, ...
  + 기사 2 : 사회, 경제, ...

- 훈련 세트와 테스트 세트


```python
fish_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
                31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
                35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0, 9.8, 
                10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
fish_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
                500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
                700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0, 6.7, 
                7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```


```python
fish_data = [[l,w] for l, w in zip(fish_length, fish_weight)]
# fish_data

# 1은 도미
# 0는 빙어
fish_target = [1]*35 + [0]*14
#fish_target
```

- 머신러닝 모델


```python
from sklearn.neighbors import KNeighborsClassifier
kn = KNeighborsClassifier()
```

### 훈련세트와 테스트 세트로 분리


```python
# 0부터 ~ 34인덱스까지 사용
# 훈련데이터 독립변수
train_input = fish_data[:35]

# 훈련데이터 종속변수
train_target = fish_target[:35]

# 테스트데이터 독립변수
test_input = fish_data[35:]

# 테스트데이터 종속변수
test_target = fish_target[35:]

#train_input.shape, train_target.shape, test_input.shape, test_target.shape
```


```python
kn = kn.fit(train_input, train_target)
kn.score(test_input, test_target)
```




    0.0




```python
fish_data[:34]
```




    [[25.4, 242.0],
     [26.3, 290.0],
     [26.5, 340.0],
     [29.0, 363.0],
     [29.0, 430.0],
     [29.7, 450.0],
     [29.7, 500.0],
     [30.0, 390.0],
     [30.0, 450.0],
     [30.7, 500.0],
     [31.0, 475.0],
     [31.0, 500.0],
     [31.5, 500.0],
     [32.0, 340.0],
     [32.0, 600.0],
     [32.0, 600.0],
     [33.0, 700.0],
     [33.0, 700.0],
     [33.5, 610.0],
     [33.5, 650.0],
     [34.0, 575.0],
     [34.0, 685.0],
     [34.5, 620.0],
     [35.0, 680.0],
     [35.0, 700.0],
     [35.0, 725.0],
     [35.0, 720.0],
     [36.0, 714.0],
     [36.0, 850.0],
     [37.0, 1000.0],
     [38.5, 920.0],
     [38.5, 955.0],
     [39.5, 925.0],
     [41.0, 975.0]]




```python
fish_target[34:]
```




    [1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]



### 샘플링 편향

### 넘파이
- 리스트로 연산은 지원이 잘 안 됨.
- 리스트를 넘파이 배열로 변환


```python
import numpy as np

input_arr = np.array(fish_data)
target_arr = np.array(fish_target)

print(input_arr.shape, target_arr.shape)    # shape 출력
```

    (49, 2) (49,)
    

- suffle : 데이터를 섞어준다
- 실험 재현성
- np.random.seed(42) 란?
  - 뒤에 42는 무의미한 수치이다.
  - 랜덤 시드이다.
  - 어떤 특정한 시작 숫자를 정해 주면 컴퓨터가 정해진 알고리즘에 의해 마치 난수처럼 보이는 수열을 생성한다.
  -  이런 시작 숫자를 시드(seed)라고 한다. 


```python
# 76p
# 랜덤 시드
np.random.seed(42)
index = np.arange(49)
index
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
           17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
           34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48])



- 셔플


```python
# 셔플 = 섞는다
np.random.shuffle(index)
print(index)
```

    [13 45 47 44 17 27 26 25 31 19 12  4 34  8  3  6 40 41 46 15  9 16 24 33
     30  0 43 32  5 29 11 36  1 21  2 37 35 23 39 10 22 18 48 20  7 42 14 28
     38]
    

- 훈련 데이터 및 테스트데이터 재 코딩


```python
train_input = input_arr[index[:35]]
train_target = target_arr[index[:35]]

print(input_arr[13], train_input[0])
```

    [ 32. 340.] [ 32. 340.]
    


```python
test_input = input_arr[index[35:]]
test_target = target_arr[index[35:]]
```


```python
train_input.shape, train_target.shape, test_input.shape, test_target.shape
```




    ((35, 2), (35,), (14, 2), (14,))



### 시각화 생략

### 두 번째 머신러닝 프로그램


```python
kn = kn.fit(train_input, train_target)
kn.score(test_input, test_target)
```




    1.0



- 다음 두 코드의 결과가 같다. 예측 성공.


```python
kn.predict(test_input)
```




    array([0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0])




```python
test_target
```




    array([0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1, 1, 0])



# 02-2 데이터 전처리

### 넘파이로 데이터 준비하기
- 다음 주소를 참고하라 : bit.ly/bream_smelt


```python
fish_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
                31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
                35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0, 9.8, 
                10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
fish_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
                500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
                700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0, 6.7, 
                7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]
```

- 2차원 리스트를 작성해보자.
- 넘파이의 column_stack() 함수는 전달받은 리스트를 일렬로 세운 다음 차례대로 나란히 연결한다.


```python
import numpy as np

np.column_stack(([1,2,3], [4,5,6]))
```




    array([[1, 4],
           [2, 5],
           [3, 6]])



- 이제 fish_length와 fish_weight를 합친다.


```python
fish_data = np.column_stack((fish_length, fish_weight))

print(fish_data[:5])
```

    [[ 25.4 242. ]
     [ 26.3 290. ]
     [ 26.5 340. ]
     [ 29.  363. ]
     [ 29.  430. ]]
    

- 동일한 방법으로 타깃 데이터도 만들어 보자.
- np.ones()와 np.zeros() 함수를 이용한다.


```python
print(np.ones(5))
```

    [1. 1. 1. 1. 1.]
    

- np.concatenate() 함수를 사용하여 첫 번째 차원을 따라 배열을 연결해보자.


```python
fish_target = np.concatenate((np.ones(35), np.zeros(14)))

print(fish_target)
```

    [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
     1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
     0.]
    

### 사이킷런으로 훈련 세트와 테스트 세트 나누기
- train_test_split()
  - 이 함수는 전달되는 리스트나 배열을 비율에 맞게 훈련 세트와 테스트 세트로 나누어 준다.
  - 사용법 : 나누고 싶은 리스트나 배열을 원하는 만큼 전달하면 된다.


```python
from sklearn.model_selection import train_test_split

train_input, test_input, train_target, test_target = train_test_split(fish_data, fish_target, random_state=42)
```

- fish_data와 fish_target 2개의 배열을 전달했으므로 2개씩 나뉘어 총 4개의 배열이 반환된다.
- 차례대로 처음 2개는 입력 데이터(train_input, test_input), 나머지 2개는 타깃 데이터(train_target, test_target)이다.
- 랜덤 시드(random_state)는 42로 지정했다.


```python
print(train_input.shape, test_input.shape)
```

    (36, 2) (13, 2)
    


```python
print(train_target.shape, test_target.shape)
```

    (36,) (13,)
    

- 훈련 데이터와 테스트 데이터를 각각 36개와 13개로 나누었다.
- 입력 데이터는 2개의 열이 있는 2차원 배열이고 타깃 데이터는 1차원 배열이다.
- 도미와 빙어가 잘 섞였는지 확인해보자.


```python
print(test_target)
```

    [1. 0. 0. 0. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
    

- 13개의 테스트 세트 중에 10개가 도미(1)이고, 3개가 빙어(0)이다.
- 빙어의 비율이 좀 모자란데, 이는 샘플링 편항때문이다.
- 이러한 문제를 train_test_split() 함수로 해결할 수 있다.
- stratify 매개변수에 타깃 데이터를 전달하면 클래스 비율에 맞게 데이터를 나누다.
- 훈련 데이터가 작거나 특정 클래스의 샘플 개수가 적을 때 특히 유용하다.


```python
train_input, test_input, train_target, test_target = train_test_split(fish_data, fish_target, stratify=fish_target, random_state=42)

print(test_target)
```

    [0. 0. 1. 0. 1. 0. 1. 1. 1. 1. 1. 1. 1.]
    

- 빙어가 하나 늘었다.
- 이전과 달리 비율이 좀 더 비슷해졌다.
- 데이터 준비가 완료되었다.

### 수상한 도미 한 마리
- 앞서 준비한 데이터로 k-최근접 이웃을 훈련해 보자.


```python
from sklearn.neighbors import KNeighborsClassifier

kn = KNeighborsClassifier()
kn.fit(train_input, train_target)
kn.score(test_input, test_target)
```




    1.0



- 완벽한 결과이다. 테스트 세트의 도미와 빙어를 모두 올바르게 분류했다.
- 이 모델에 문제가 되었던 도미 데이터를 넣고 결과를 확인해본다.


```python
print(kn.predict([[25, 150]]))
```

    [0.]
    

- 도미 데이터인데 빙어로 나왔다.
- 산점도로 다시 확인해보자.


```python
import matplotlib.pyplot as plt
plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')  # marker 매개변수는 모양을 지정한다. '^'는 삼각형.
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter2_김민균/output_55_0.png)
    


- 새로운 샘플은 marker 매개변수를 이용하여 삼각형으로 표시했다.
- 샘플은 오른쪽의 도미와 가까운 위치에 있는데 어째서 빙어로 판단했을까?
- k-최근접 이웃은 주변의 샘플 중에서 다수인 클래스를 예측으로 사용한다.
- KNeighborsClassifier클래스는 주어진 샘플에서 가장 가까운 이웃을 찾아 주는 kneighbors() 메서드를 제공한다.
  - 이 클래스의 이웃 개수인 n-neighbors의 기본값은 5이므로 5개의 이웃이 반환된다.


```python
distances, indexes = kn.kneighbors([[25, 150]])
```

- indexes 배열을 사용해 훈련 데이터 중에서 이웃 샘플을 따로 구분해 그려본다.


```python
plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')
plt.scatter(train_input[indexes,0], train_input[indexes,1], marker='D')   # 'D' 는 마름모 모양으로 출력
plt.xlabel('length')
plt.ylabel('weight')
```




    Text(0, 0.5, 'weight')




    
![png](/images/chapter2_김민균/output_59_1.png)
    


- marker='D'로 지정하면 산점도를 마름모로 그린다.
- 삼각형 샘플에 가장 가까운 5개의 샘플이 초록 다이아몬드로 표시되었다.
- 가장 가까운 이웃에 도미가 하나밖에 포함되지 않았다.


```python
print(train_input[indexes])
```

    [[[ 25.4 242. ]
      [ 15.   19.9]
      [ 14.3  19.7]
      [ 13.   12.2]
      [ 12.2  12.2]]]
    

- 가장 가까운 생선 4개는 빙어(0)인 것 같다.
- 타깃 데이터로 확인하면 더 명확하다.


```python
print(train_target[indexes])
```

    [[1. 0. 0. 0. 0.]]
    

- 해당 문제 해결의 실마리를 위해 distance배열을 출력해본다.
- 이 배열에는 이웃 샘플까지의 거리가 담겨 있다.


```python
print(distances)
```

    [[ 92.00086956 130.48375378 130.73859415 138.32150953 138.39320793]]
    

### 기준을 맞춰라
- 산점도를 다시 살펴본다.
- 삼각형 샘플과 근처 5개 샘플 사이의 거리가 이상하다.
- 가장 가까운 것과의 거리가 92이고, 그 나머지는 두 배 이상 멀어보이는데 수치는 그렇지 않다.
- 이는 x의 범위가 좁고 y축의 범위가 넓기에 그렇게 보이는 것이다.
- 명확하게 보기 위해 x축의 범위를 동일하게 맞춘다.
  - xlim()함수를 사용하여 x축 범위를 지정한다.



```python
plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')
plt.scatter(train_input[indexes,0], train_input[indexes,1], marker='D')
plt.xlim((0, 1000)) # x축 지정
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter2_김민균/output_67_0.png)
    


- 두 특성(길이와 무게)의 값이 놓인 범위가 매우 다르다.
- 이를 투 특성의 스케일(scale)이 다르다고 한다.


### 데이터 전처리
- 데이터를 표현하는 기준이 다르면 알고리즘이 올바르게 예측할 수 없다.
- 알고리즘이 거리 기반일 때 특히 그렇다. 여기에는 k-최근접 이웃도 포함된다.
- 이런 알고리즘들은 샘플 간의 거리에 영향을 많이 받으므로 제대로 사요하려면 특성값을 일정한 기준으로 맞춰 주어야 한다.
- 이런 작업을 데이터 전처리(data preprocessing)이라고 부른다.

- 표준 점수
  - 가장 널리 사용하는 전처리 방법 중 하나는 표준점수(standatd score)이다.
  - 표준점수는 각 특성값이 평균에서 표준편차의 몇 배만큼 떨어져 있는지를 나타낸다.
  - 이를 통해 실제 특성값의 크기와 상광없이 동일한 조건으로 비교할 수 있다


```python
mean = np.mean(train_input, axis=0)
std = np.std(train_input, axis=0)
```

- np.mean() 함수는 평균을 계산하고, np.std() 함수는 표준편차를 계산한다.
- axis=0으로 지정했으며, 이렇게 하면 행을 따라 각 열의 통계 값을 계산한다.


```python
print(mean, std)
```

    [ 27.29722222 454.09722222] [  9.98244253 323.29893931]
    

- 각 특성마다 평균과 표준편차가 구해졌다.
- 이제 원본 데이터에서 평균을 빼고 표준편차로 나누어 표준점수로 변환한다.


```python
train_scaled = (train_input - mean) / std
```

- 브로드 캐스팅 (breadcastion)
  - 이 식은 어떻게 계산될까?
  - 넘파이는 train_input의 모든 행에서 mean에 있는 두 평균값을 뺀다.
  - 그 다은 std에 있는 두 표준편차를 모든 행에 적용한다.
  - 이런 넘파이 기능을 브로드캐스팅이라고 부른다.

### 전처리 데이터로 모델 훈련하기
- 앞에서 표준점수로 변환한 train_scaled를 만들었다.
- 다시 샘플을 산점도로 그려보자.


```python
plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(25, 150, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter2_김민균/output_78_0.png)
    


- 우측 상단에 샘플 하나가 덩그러니 떨어져 있다.
- 훈련 세트를 mean(평균)으로 빼고 std(표준편차)로 나누어 주었기 때문에 값의 범위가 달라졌다.
- 동일한 기준으로 샘플을 변환하고 다시 산점도를 그려보자.


```python
new = ([25, 150] - mean) / std
plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter2_김민균/output_80_0.png)
    


- 훈련 데이터의 두 특성이 비슷한 범위를 차지하고 있다.
- 이제 이 데이터셋으로 k-최근접 이웃 모델을 다시 훈련해 보자.


```python
kn.fit(train_scaled, train_target)
```




    KNeighborsClassifier()



- 테스트 세트의 스케일을 변환해 보자.


```python
test_scaled = (test_input - mean) / std
```

- 이제 모델을 평가한다.


```python
kn.score(test_scaled, test_target)
```




    1.0



- 완벽하다. 모든 테스트 세트의 샘플을 완벽하게 분류했다.
- 앞서 훈련 세트의 평균고 표준편차로 변환한 김 팀장의 샘플 사용해 모델의 예측을 출력해보자.


```python
print(kn.predict([new]))
```

    [1.]
    

- 드디어 도미(1)로 예측했다. 확일시 길이가 25cm이고 무게가 150g인 생선은 도미일 것이다.
- 마지막으로 keighbors()함수로 이 샘플의 k-최근점 이웃을 구한 다음 산점도로 그려보자.
- 특성을 표준점수로 바꾸었기 때문에 알고리즘이 올바르게 거리를 측정했을 것이다.


```python
distances, indexes = kn.kneighbors([new])
plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')
plt.scatter(train_scaled[indexes,0], train_scaled[indexes,1], marker='D')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```


    
![png](/images/chapter2_김민균/output_90_0.png)
    


- 삼각형 샘플에서 가장 가까운 샘플은 모두 도미이다.
- 따라서 이 수상한 샘플을 도미로 예측하는 것이 당연하다.
- 성공이다. 특성값의 스케일에 민감하지 않고 안정적인 예측을 할 수 있는 모델을 만들었다.

### 전체 소스 코드
- 다음 주소를 참고하라 : bit.ly/hg-02-2


```python
fish_length = [25.4, 26.3, 26.5, 29.0, 29.0, 29.7, 29.7, 30.0, 30.0, 30.7, 31.0, 31.0, 
                31.5, 32.0, 32.0, 32.0, 33.0, 33.0, 33.5, 33.5, 34.0, 34.0, 34.5, 35.0, 
                35.0, 35.0, 35.0, 36.0, 36.0, 37.0, 38.5, 38.5, 39.5, 41.0, 41.0, 9.8, 
                10.5, 10.6, 11.0, 11.2, 11.3, 11.8, 11.8, 12.0, 12.2, 12.4, 13.0, 14.3, 15.0]
fish_weight = [242.0, 290.0, 340.0, 363.0, 430.0, 450.0, 500.0, 390.0, 450.0, 500.0, 475.0, 500.0, 
                500.0, 340.0, 600.0, 600.0, 700.0, 700.0, 610.0, 650.0, 575.0, 685.0, 620.0, 680.0, 
                700.0, 725.0, 720.0, 714.0, 850.0, 1000.0, 920.0, 955.0, 925.0, 975.0, 950.0, 6.7, 
                7.5, 7.0, 9.7, 9.8, 8.7, 10.0, 9.9, 9.8, 12.2, 13.4, 12.2, 19.7, 19.9]

import numpy as np

np.column_stack(([1,2,3], [4,5,6]))

fish_data = np.column_stack((fish_length, fish_weight))
print(fish_data[:5])
print(np.ones(5))

fish_target = np.concatenate((np.ones(35), np.zeros(14)))
print(fish_target)

from sklearn.model_selection import train_test_split

train_input, test_input, train_target, test_target = train_test_split(
    fish_data, fish_target, random_state=42)
print(train_input.shape, test_input.shape)
print(train_target.shape, test_target.shape)
print(test_target)

train_input, test_input, train_target, test_target = train_test_split(
    fish_data, fish_target, stratify=fish_target, random_state=42)
print(test_target)

from sklearn.neighbors import KNeighborsClassifier

kn = KNeighborsClassifier()
kn.fit(train_input, train_target)
kn.score(test_input, test_target)

print(kn.predict([[25, 150]]))

import matplotlib.pyplot as plt

plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

distances, indexes = kn.kneighbors([[25, 150]])

plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')
plt.scatter(train_input[indexes,0], train_input[indexes,1], marker='D')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

print(train_input[indexes])
print(train_target[indexes])
print(distances)

plt.scatter(train_input[:,0], train_input[:,1])
plt.scatter(25, 150, marker='^')
plt.scatter(train_input[indexes,0], train_input[indexes,1], marker='D')
plt.xlim((0, 1000))
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

mean = np.mean(train_input, axis=0)
std = np.std(train_input, axis=0)

print(mean, std)

train_scaled = (train_input - mean) / std

plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(25, 150, marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

new = ([25, 150] - mean) / std

plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()

kn.fit(train_scaled, train_target)

test_scaled = (test_input - mean) / std

kn.score(test_scaled, test_target)

print(kn.predict([new]))

distances, indexes = kn.kneighbors([new])

plt.scatter(train_scaled[:,0], train_scaled[:,1])
plt.scatter(new[0], new[1], marker='^')
plt.scatter(train_scaled[indexes,0], train_scaled[indexes,1], marker='D')
plt.xlabel('length')
plt.ylabel('weight')
plt.show()
```

    [[ 25.4 242. ]
     [ 26.3 290. ]
     [ 26.5 340. ]
     [ 29.  363. ]
     [ 29.  430. ]]
    [1. 1. 1. 1. 1.]
    [1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1.
     1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 1. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.
     0.]
    (36, 2) (13, 2)
    (36,) (13,)
    [1. 0. 0. 0. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
    [0. 0. 1. 0. 1. 0. 1. 1. 1. 1. 1. 1. 1.]
    [0.]
    


    
![png](/images/chapter2_김민균/output_93_1.png)
    



    
![png](/images/chapter2_김민균/output_93_2.png)
    


    [[[ 25.4 242. ]
      [ 15.   19.9]
      [ 14.3  19.7]
      [ 13.   12.2]
      [ 12.2  12.2]]]
    [[1. 0. 0. 0. 0.]]
    [[ 92.00086956 130.48375378 130.73859415 138.32150953 138.39320793]]
    


    
![png](/images/chapter2_김민균/output_93_4.png)
    


    [ 27.29722222 454.09722222] [  9.98244253 323.29893931]
    


    
![png](/images/chapter2_김민균/output_93_6.png)
    



    
![png](/images/chapter2_김민균/output_93_7.png)
    


    [1.]
    


    
![png](/images/chapter2_김민균/output_93_9.png)
    


- Reference : 혼자 공부하는 머신러닝 + 딥러닝
