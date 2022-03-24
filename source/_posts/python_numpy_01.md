---
title: "python_numpy_01"
tags:
  - python
categories:
  - python
  - library
  - numpy
author: "minkuen"
date: '2022-03-23'
---

# 라이브러리
- 여러가지 라이브러리를 사용해보자

# Numpy
Q : what is numpy?

A : 배열 연산이다.

Q : why numpy?

A : 두개의 리스트 연산 시도 → Type Error → Numpy 도입


```python
# 다음 코드는 사용 시 error가 나온다.
A = [1, 2, 3]
B = [4, 5, 6]

A / B ** 2
```


```python
# numpy 사용 시 정상적으로 작동한다.
import numpy as np

A = [1, 2, 3]
B = [4 ,5, 6]

np_A = np.array(A)
np_B = np.array(B)
np_A / np_B ** 2
```




    array([0.0625    , 0.08      , 0.08333333])



### Reshape

사용 예시 
- (2,3) 배열 -> np.reshape(3,2) -> (3,2)배열

사용 예시
- np.reshape(-1, 2)에서 -1의 의미
: 특정 차원에서 열은 2로 고정된 상태에서 행은 사이즈에 맞도록 자동으로 정렬해준다는 뜻


```python
import numpy as np
temp_arr = np.array([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16])
temp_arr

new_arr = temp_arr.reshape(2, -1)
new_arr
```




    array([[ 1,  2,  3,  4,  5,  6,  7,  8],
           [ 9, 10, 11, 12, 13, 14, 15, 16]])




```python
# -1을 이용한 자동 정렬
new_arr = temp_arr.reshape(4, -1)
new_arr
```




    array([[ 1,  2,  3,  4],
           [ 5,  6,  7,  8],
           [ 9, 10, 11, 12],
           [13, 14, 15, 16]])



조언
- 머신러닝 / 딥러닝
  - 수학을 잘 하는 사람 vs 수학을 처음 하는 사람
  - 머신러닝 / 딥러닝 (인간이 만든 수식!)
  - 개념을 이해하고, 수식으로 이해하고, 코드로 그 수식을 구현해야
  - 머신러닝과 딥러닝을 쓰기 위해서는 수학자만 해야되냐!?
  - 결론은 아닙니다!
  - 머신러닝 / 딥러닝의 주 목적이 인간 생활의 보편적인 무제 해결을 위해 나온 것
  - 프레임워크로 형태로 내놨어요 (개념을 이해하고 있자!)
    - 개념만 문자열 타입으로 매개변수를 잘 조정만 하면 모델 만들어짐!
  - 성과를 내야 하는데 (개발자는 배포를 잘해야 함!)
    - 이미지 인식 모델을 만듬 / (쓸데가 없음...) / 안드로이드 앱 / 웹앱에 탑재할줄만 알아도
    - 기획 (어떤 문데를 풀까?)
  - AutoML
    - 코드를 4 ~ 5줄 치면 머신러닝 모델이 만들어짐!  
    - 하지만 이공계 출신이라면 수식도 나름대로 정리해 볼 것



라이브러리 설치 방법 (vs R)


```python
# R install.packages("패키지명")
# 파이썬 라이브러리 설치 코드에서 실행 (X)
# 터미널에서 설치

# 방법1. conda 설치
# --> 아나콘다 설치 후, conda 설치 (데이터 과학)
# conda 라이브러리 관리 (버전 업데이트가 조금 느림)

# 방법2. pip 설치
# --> 아나콘다 설치 안 함 / 파이썬만 설치

# git bash 열고, pip install numpy
#pip install numpy
# google colab에선 기본적 환경이 갖추어져 있음.
```

Numpy 라이브 불러오기


```python
# 다음과 같이 np 라고 줄여서 출력한다.
import numpy as np
print(np.__version__)
```

    1.21.5
    

### 배열로 변환 
- 1부터 10까지의 리스트를 만든다.
- Numpy 배열로 변환해서 저장한다.


```python
temp = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr = np.array(temp)
print(arr)
print(temp)
```

    [ 1  2  3  4  5  6  7  8  9 10]
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    


```python
print(type(arr))
print(type(temp))
```

    <class 'numpy.ndarray'>
    <class 'list'>
    

- Numpy를 사용하여 기초 통계 함수를 사용한다.


```python
print(np.mean(arr))
print(np.sum(arr))
print(np.median(arr))
print(np.std(arr))
```

    5.5
    55
    5.5
    2.8722813232690143
    

### 사칙연산


```python
math_scores = [90,80, 88]
english_scores = [80, 70, 90]

total_scores = math_scores + english_scores
total_scores
```




    [90, 80, 88, 80, 70, 90]




```python
math_scores = [90,80, 88]
english_scores = [80, 70, 90]

math_arr = np.array(math_scores)
english_arr = np.array(english_scores)

total_scores = math_arr + english_arr
total_scores
```




    array([170, 150, 178])




```python
np.min(total_scores)
```




    150




```python
np.max(total_scores)
```




    178




```python
math_scores = [2, 3, 4]
english_scores = [1, 2, 3]

math_arr = np.array(math_scores)
english_arr = np.array(english_scores)

#사칙연산
print("덧셈 : ", np.add(math_arr, english_arr))
print("뺄셈 : ", np.subtract(math_arr, english_arr))
print("곱셈 : ", np.multiply(math_arr, english_arr))
print("나눗셈 : ", np.divide(math_arr, english_arr))
print("거듭제곱 : ", np.power(math_arr, english_arr))
```

    덧셈 :  [3 5 7]
    뺄셈 :  [1 1 1]
    곱셈 :  [ 2  6 12]
    나눗셈 :  [2.         1.5        1.33333333]
    거듭제곱 :  [ 2  9 64]
    

### 배열의 생성
- 0차원부터 3차원까지 생성하는 방법


```python
temp_arr = np.array(20)
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
```

    20
    <class 'numpy.ndarray'>
    ()
    


```python
# 1차원 배열
temp_arr = np.array([1,2,3])
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape) # 배열의 형태 확인용
print(temp_arr.ndim)  # ndim은 차원 확인용
```

    [1 2 3]
    <class 'numpy.ndarray'>
    (3,)
    1
    


```python
# 2차원 배열
temp_arr = np.array([[1,2,3], [4, 5, 6]])
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
print(temp_arr.ndim)  # ndim 은 차원 확인
```

    [[1 2 3]
     [4 5 6]]
    <class 'numpy.ndarray'>
    (2, 3)
    2
    


```python
# 3차원 배열
temp_arr = np.array([[[1,2,3], [4, 5, 6]], [[1,2,3], [4, 5, 6]]])
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
print(temp_arr.ndim)  # ndim 은 차원 확인
```

    [[[1 2 3]
      [4 5 6]]
    
     [[1 2 3]
      [4 5 6]]]
    <class 'numpy.ndarray'>
    (2, 2, 3)
    3
    


```python
temp_arr = np.array([1, 2, 3, 4], ndmin = 2) # 차원을 변경 가능
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
print(temp_arr.ndim)
```

    [[1 2 3 4]]
    <class 'numpy.ndarray'>
    (1, 4)
    2
    

### 소수점 정렬


```python
temp_arr = np.trunc([-1.23, 1.23])
temp_arr
```




    array([-1.,  1.])




```python
temp_arr = np.fix([-1.23, 1.23])
temp_arr
```




    array([-1.,  1.])




```python
# 반올림
temp_arr = np.around([-1.63789, 1.23784], 4)  # 소수점 아래 4번째자리로 반올림 한다는 표현
temp_arr
```




    array([-1.6379,  1.2378])




```python
# 올림
temp_arr = np.floor([-1.63789, 1.23784])
temp_arr
```




    array([-2.,  1.])




```python
# 내림
temp_arr = np.ceil([-1.63789, 1.23784])
temp_arr
```




    array([-1.,  2.])



* shape 높이 * 세로 * 가로 순인건가요?
* axis 축 설정

### 배열을 사용하는 다양한 방법들


```python
# np.arange(5) -> 0 부터 시작하는 5개의 배열 생성
temp_arr = np.arange(5)
temp_arr
```




    array([0, 1, 2, 3, 4])




```python
# np.arange(1, 11, 3) -> 1 부터 11까지 3만큼 차이나게 배열 생성
temp_arr = np.arange(1, 11, 3)
temp_arr
```




    array([ 1,  4,  7, 10])




```python
# np.zeros -> 0으로 채운 배열 만들기
zero_arr = np.zeros((2,3))
print(zero_arr)
print(type(zero_arr))
print(zero_arr.shape)
print(zero_arr.ndim)
print(zero_arr.dtype) # dype = data type
```

    [[0. 0. 0.]
     [0. 0. 0.]]
    <class 'numpy.ndarray'>
    (2, 3)
    2
    float64
    


```python
# np.ones -> 1로 채운 배열 만들기
temp_arr = np.ones((4,5), dtype="int32")  
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
print(temp_arr.ndim)
print(temp_arr.dtype)
```

    [[1 1 1 1 1]
     [1 1 1 1 1]
     [1 1 1 1 1]
     [1 1 1 1 1]]
    <class 'numpy.ndarray'>
    (4, 5)
    2
    int32
    


```python
temp_arr = np.ones((2,6), dtype="int32")  
print(temp_arr)
print(type(temp_arr))
print(temp_arr.shape)
print(temp_arr.ndim)
print(temp_arr.dtype)
```

    [[1 1 1 1 1 1]
     [1 1 1 1 1 1]]
    <class 'numpy.ndarray'>
    (2, 6)
    2
    int32
    


```python
# reshape() 사용하여 배열 변환하기 
temp_arr = np.ones((12,12), dtype="int32")  
temp_res_arr = temp_arr.reshape(4, -1)    # -1 은 자동정령
print(temp_res_arr)
print(type(temp_res_arr))
print(temp_res_arr.shape)
print(temp_res_arr.ndim)
print(temp_res_arr.dtype)
```

    [[1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1]
     [1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1]
     [1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1]
     [1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1]]
    <class 'numpy.ndarray'>
    (4, 36)
    2
    int32
    

### numpy 조건식
- where(a, b, c) 사용법
  -  a조건 True면 b로 변환, False이면 c로 변환


```python
temp_arr = np.arange(10)
temp_arr
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
# 5보다 작은 값은 원래값으로 변환
# 5보다 큰 값은 원래 값 * 10
np.where(temp_arr <5, temp_arr, temp_arr * 10)

#  where(a, b, c) a조건 True면 b로 변환, False이면 c로 변환
```




    array([ 0,  1,  2,  3,  4, 50, 60, 70, 80, 90])




```python
# 0~100 까지의 배열 만들고, 50보다 작은 값은 곱하기 10, 나머지는 그냥 원래 값으로 반환
temp_arr = np.arange(101)
temp_arr

np.where(temp_arr <50, temp_arr * 10, temp_arr)
```




    array([  0,  10,  20,  30,  40,  50,  60,  70,  80,  90, 100, 110, 120,
           130, 140, 150, 160, 170, 180, 190, 200, 210, 220, 230, 240, 250,
           260, 270, 280, 290, 300, 310, 320, 330, 340, 350, 360, 370, 380,
           390, 400, 410, 420, 430, 440, 450, 460, 470, 480, 490,  50,  51,
            52,  53,  54,  55,  56,  57,  58,  59,  60,  61,  62,  63,  64,
            65,  66,  67,  68,  69,  70,  71,  72,  73,  74,  75,  76,  77,
            78,  79,  80,  81,  82,  83,  84,  85,  86,  87,  88,  89,  90,
            91,  92,  93,  94,  95,  96,  97,  98,  99, 100])



### 두가지 조건식을 사용해야 할 경우
- np.select
- 사용법은 다음 코드를 참고


```python
temp_arr = np.arange(10)
temp_arr

# 5보다 큰 값은 곱하기 2, 2보다 작은 값은 더하기 100
condlist = [temp_arr > 5, temp_arr <2]    # 조건식
choielist = [temp_arr *2, temp_arr + 100] # 같은 위치의 조건 만족 시, 설정한 대로 변환
np.select(condlist, choielist, default = temp_arr)
```




    array([100, 101,   2,   3,   4,   5,  12,  14,  16,  18])



### 브로드캐스팅
- 서로 다른 크기의 배열을 계산할 때 참고해야하는 내용이다.
