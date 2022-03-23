---
title: "파이썬_기초문법_2"
tags:
  - python
categories:
  - python
  - 기초문법
  - 함수
author: "minkuen"
date: '2022-03-22'
---

# 기초 문법 리뷰

```python
# 리스트
book_list = ["A", "B", "C"]
# append, extend, insert, remove, pop, etc

# 튜플
book_tuple = ("A", "B", "C")
# 수정 삭제가 불가능하다

# 딕셔너리
book_dictionary = {"책 제목" : ["A", "B"], "출판년도" : [2011, 2002]}
# keys(), values(), items(), get()
```

## 조건문 & 반복문


```python
if True:
  print("코드 실행")
elif True:
  print("코드 실행")
else:
  print("코드 실행")
```


```python
for idx in range(3):
  print(idx+1, "안녕하세요")
```

    1 안녕하세요
    2 안녕하세요
    3 안녕하세요
    


```python
book_list = ["프로그래밍 R", "혼자 공부하는 머신러닝"]
for book in book_list:
  print(book)
```

    프로그래밍 R
    혼자 공부하는 머신러닝
    


```python
strings01 = "Hello world"
for char in strings01:
  print(char)
```


```python
num_tuple = (1, 2, 3, 4)
for num in num_tuple:
  print(num)
```

    1
    2
    3
    4
    


```python
num_dict = {"A" : 1, "B" : 2}
for num in num_dict:
  print(num)
  print(num_dict[num])
```

    A
    1
    B
    2
    

### 반복문의 필요성


```python
product_name = ["요구르트", "우유", "과자"]
prices = [1000, 1500, 2000]
quantities = [5, 3, 4]

name = product_name[0]
sales = prices[0] * quantities[0]
print(name + "의 매출액은 " + str(sales) + "원이다.")

name = product_name[1]
sales = prices[1] * quantities[1]
print(name + "의 매출액은 " + str(sales) + "원이다.")

# 위 코드의 반복문 코드 작성 필요 절감

for num in range(len(product_name)):
  name = product_name[num]
  sales = prices[num] * quantities[num]
  print(name + "의 매출액은 " + str(sales) + "원이다.")
```

    요구르트의 매출액은 5000원이다.
    우유의 매출액은 4500원이다.
    요구르트의 매출액은 5000원이다.
    우유의 매출액은 4500원이다.
    과자의 매출액은 8000원이다.
    

## while
- 조건식이 들어간 반복문
(vs for-loop 범위!!!)


```python
count = 1
while count < 5:
  count = count + 1
  print("안녕하세요..")

print("5 초과했군요..")
```

    안녕하세요..
    안녕하세요..
    안녕하세요..
    안녕하세요..
    5 초과했군요..
    


```python
count = 3
while count > 0:
  print("안녕하세요..")
  count = count - 1
  print(count)

print("0 미만이군요..")
```

    안녕하세요..
    2
    안녕하세요..
    1
    안녕하세요..
    0
    0 미만이군요..
    

- 개발자를 지향한다!
  + while 공부 좀 더 비중 있게 다루는 걸 추천
- 데이터 분석
  + for-loop 공부를 좀 더 비중있게 하는 것 추천

# 사용자 정의 함수 (User-Defined Function)
- why?

### 클래스(Class)를 왜 쓸까?
- 코드의 반복성을 줄이기 위해서 사용!

### len() --> 누군가가 만들었고, 우리는 그걸 그냥 쓰는 것
- 리스트의 길이 구할 때 사용
- 리스트 전체 길이를 구하겠다!? --> 1회성? 나만 쓰는가? no





```python
def 함수명():
  #코드 실행
  return 값

함수명()
```


```python
def add(a, b):
  """정수 2개를 입력받아 더하는 함수입니다.

  Args:
    a(int) : 계산할 정수
    b(int) : 계산할 정수
    c(int) : 계산 결과
 
  Returns:
    int
  """
  c = a + b
  return c
add(1,2)


def minus(a,b):
  """정수 2개를 입력받아 빼는 함수입니다.

  Args:
    a(int) : 계산할 정수
    b(int) : 계산할 정수
    c(int) : 계산 결과
 
  Returns:
    int
  """
  c = a - b
  return c
minus(10, 5)


def multiple(a,b):
  """정수 2개를 입력받아 곱하는 함수입니다.

  Args:
    a(int) : 계산할 정수
    b(int) : 계산할 정수
    c(int) : 계산 결과
 
  Returns:
    int
  """
  c = a * b
  return c
multiple(10,5)


def divide(a,b):
  """정수 2개를 입력받아 나누는 함수입니다.

  Args:
    a(int) : 계산할 정수
    b(int) : 계산할 정수
    c(float) : 계산 결과
 
  Returns:
    float
  """
  c = a / b
  return c
divide(10,5)

if __name__ == "__main__":
  print("add(10,5) = ", add(10,5) )
  print("minus(10,5) = ", minus(10,5) )
  print("multiple(10,5) = ", multiple(10,5) )
  print("divide(10,5) = ", divide(10,5) )
```

    add(10,5) =  15
    minus(10,5) =  5
    multiple(10,5) =  50
    divide(10,5) =  2.0
    


```python

def minus(a,b):
  """정수 2개를 입력받아 빼는 함수입니다.

  Args:
    a(int) : 계산할 정수
    b(int) : 계산할 정수
    c(int) : 계산 결과
 
  Returns:
    int
  """
  c = a - b
  return c
minus(10, 5)
```

jupyter notebook, ipynb 파일명

.py로 저장(PyCharm..)


```python
!which pyhon
```

basic.py로 저장할 때, 예시


```python
# /usr/local/bin/python
# -*- coding: utf-8 -*- 

def temp(content, letter):
  """content 안에 있는 문자를 세는 함수입니다.

  Args:
    content(str) : 탐색 문자열
    letter(str) : 찾을 문자열

  Returns:
    int
  """
  print("함수 테스트")

  cnt = len([char for char in content if char == letter])
  return cnt

if __name__ == "__main__":
  help(temp)
  docstring = temp.__doc__
  print(docstring)
```

    Help on function temp in module __main__:
    
    temp(content, letter)
        content 안에 있는 문자를 세는 함수입니다.
        
        Args:
          content(str) : 탐색 문자열
          letter(str) : 찾을 문자열
        
        Returns:
          int
    
    content 안에 있는 문자를 세는 함수입니다.
    
      Args:
        content(str) : 탐색 문자열
        letter(str) : 찾을 문자열
    
      Returns:
        int
      
    

### help()
- 위 코드에서 help()는 본인이 작성한 주석을 바탕으로 문서화한다.

## 리스트 컴프리헨션
- for-loop 반복문을 한 줄로 처리
- 리스트 안에 반복문을 작성할 수 있다


```python
my_list = [[10], [20,30]]
print(my_list)

flattened_list = []
for value_list in my_list:
  print(value_list)
  for value in value_list:
    print(value)
    flattened_list.append(value)

print(flattened_list)

# 결괏값 : return[10 ,20, 30]
```

    [[10], [20, 30]]
    [10]
    10
    [20, 30]
    20
    30
    [10, 20, 30]
    


```python
my_list = [[10], [20, 30]]
flattened_list = [value for value_list in my_list for value in value_list]   # 리스트 컴프리헨션
print(flattened_list)
```

    [10, 20, 30]
    


```python
letters = []
for char in "helloworld":
  letters.append(char)
print(letters)
```

    ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
    


```python
letters2 = [char for char in "helloworld"]  # 리스트 컴프리헨션
print(letters)
```

    ['h', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd']
    


```python
value_list = [1, 2, 3, 4, 5, 6]
print("avg: ", sum(value_list) / len(value_list))
# 중간값

midpoint = int(len(value_list) / 2)
#len(value_list) % 2 == 0;
print((value_list[midpoint -1 ] + value_list[midpoint]) / 2)
print(value_list[midpoint])

```

    avg:  3.5
    3.5
    4
    


```python
# 사용자 정의함수의 문서화
def mean_and_median(value_list):
  """ 숫자 리스트의 요소들의 평균과 중간값을 구하는 코드를 작성해라
  Args:
    value_list (iterable of int / float) : A list of int numbers

  Returns:
    tuple(float, float)
  """
  #평균
  mean = sum(value_list) / len(value_list)

  #중간값
  midpoint = int(len(value_list) / 2)
  if len(value_list) % 2 == 0:
    median = (value_list[midpoint - 1] + value_list[midpoint]) / 2
  else:
    median = value_list[midpoint]
  
  return mean, median

if __name__ == "__main__":
  value_list = [1, 1, 2, 2, 3, 4, 5]
  avg, median = mean_and_median(value_list)
  print("avg : ", avg)
  print("median", median)
```

    avg :  2.5714285714285716
    median 2
    

- 데코레이터, 변수명 immutable or mutable, context manager는
jump to python 페이지에 없기에 따로 찾아 공부해야 한다.

# 함수 실습

### 여러 개의 입력값을 받는 함수


```python
# 여러 개의 입력값을 받는 함수 만들기
def add_many(*args):
  result = 0
  for i in args:
    result = result + i
  return result

```


```python
# 위 함수를 이용해보자
result = add_many(1,2,3)
print(result)

#위 함수는 매개변수가 몇 개든 작동한다.
result = add_many(1,2,3,4,5,6,7,8,9,10)
print(result)
```

    6
    55
    


```python
# 여러 개의 입력값을 받는 함수 만들기2
def add_mul(choice, *args):
  if choice == "add":
    result=0
    for i in args:
      result = result + i
  elif choice == "mul":
      result = 1
      for i in args:
        result = result * i
  return result
```


```python
# 위 함수를 이용해보자
result = add_mul('add', 1, 2, 3, 4, 5)
print(result)

result = add_mul('mul', 1, 2, 3, 4, 5)
print(result)
```

    15
    120
    

### 키워드 파라미터 kwargs
- 키워드 파라미터를 사용할 때는 매개변수 앞에 별 두 개(**)를 붙인다.


```python
# 매개변수 kwargs를 출력하는 함수이다.
def print_kwargs(**kwargs):
  print(kwargs)

# 위 함수를 사용해보자
print_kwargs(a=1)
print_kwargs(name='foo', age=3)
{'age': 3, 'name': 'foo'}

# **을 붙이면 매개변수 kwargs는 딕셔너리가 되고 모든 key=value 형태의 결괏값이 그 딕셔너리에 저장된다.
```

    {'a': 1}
    {'name': 'foo', 'age': 3}
    




    {'age': 3, 'name': 'foo'}



### 매개변수에 초깃값 미리 설정하기


```python
def say_myself(name, old, man=True):    # boolean 값을 이용하여 설정
  print("나의 이름은 %s 입니다." % name)
  print("나이는 %d살입니다." % old)
  if man :
    print("남자입니다.")  # True
  else :
    print("여자입니다.")  # False

say_myself("박응용", 27)
say_myself("박응용", 27, True)
say_myself("박응용", 27, False)
```

    나의 이름은 박응용 입니다.
    나이는 27살입니다.
    남자입니다.
    나의 이름은 박응용 입니다.
    나이는 27살입니다.
    남자입니다.
    나의 이름은 박응용 입니다.
    나이는 27살입니다.
    여자입니다.
    

### 함수 안에서 선언한 변수의 효력 범위


```python
a = 1
def vartest(a):
    a = a +1

vartest(a)
print(a)

# 결과 = 1
# 즉 함수 안에서 사용하는 매개변수는 함수 밖의 변수 이름과는 전혀 상관이 없다는 뜻이다.
```

    1
    

### 함수 안에서 함수 밖의 변수를 변경하는 방법
- 1. return 사용하기
- 2. global 사용하기


```python
# return 사용하기
a = 1
def vartest(a):
  a = a + 1
  return a    # return으로 값 반환
  
a = vartest(a)
print(a)
```

    2
    


```python
# global 사용하기
a = 1
def vartest():
  global a
  a = a + 1

vartest()   #효과는 있지만, 가급적 사용하지 말자.
print(a)
```

    2
    

### lambda
- 함수를 생성할 때 사용하는 예약어로 def와 동일한 역할을 한다. 
- 보통 함수를 한줄로 간결하게 만들 때 사용


```python
add = lambda a, b : a+b
result = add(3,4)
print(result)
```

    7
    

## 사용자 입력과 출력

### 사용자 입력
- input 사용


```python
number1 = input("숫자를 입력하세요... : ")
print(number1)    # 문자열 취급이므로 주의

number2 = int(input("숫자를 입력하세요... : "))
print(number2)    # int로 형변환하여 정수 취급됨.

```

    숫자를 입력하세요... : 1
    1
    숫자를 입력하세요... : 4
    4
    

### print 자세히 알기


```python
# 큰따옴표로 둘러싸인 문자열은 + 연산과 동일하다
print("life" "is" "too short")
print("life" + "is" + "too short")
```

    lifeistoo short
    lifeistoo short
    


```python
# 문자열 띄어쓰기는 콤마로 한다
print("life", "is", "too short")
```

    life is too short
    


```python
# 한 줄에 결괏값 출력하기
for i in range(10):
  print(i, end=' ')   
  # 매개변수 end를 사용하여 끝 문자를 지정
```

    0 1 2 3 4 5 6 7 8 9 

## 파일 생성하기
- 파일 열기 모드에는 다음과 같은 것이 있다.
  - r : 읽기모드 - 파일을 읽기만 할 때 사용
  - w : 쓰기모드 - 파일에 내용을 쓸 때 사용
  - a : 추가모드 - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용


```python
f = open("새파일.txt", 'w')
f.close()
```


```python
# 만약 새파일.txt 파일을 C:/doit 디렉터리에 생성하고 싶다면 다음과 같이 작성
f = open("C:/doit/새파일.txt", 'w')
f.close()
```


```python
# 파일을 쓰기 모드로 열어 출력값 적기
f = open("C:/doit/새파일.txt", 'w')
for i in range(1, 11):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```


```python
# 파일에 새로운 내용 추가하기
f = open("C:/doit/새파일.txt",'a')
for i in range(11, 20):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```

# 4장 연습문제


```python
# Q1 주어진 자연수가 홀수인지 짝수인지 판별해 주는 함수(is_odd)를 작성해 보자.

def is_odd(n):
  if n%2 ==0 :
    print("짝수입니다...")
  else :
    print("홀수입니다...")

num = int(input("자연수를 입력하세요...: "))
is_odd(num)
```

    자연수를 입력하세요...: 3
    홀수입니다...
    


```python
# Q2 입력으로 들어오는 모든 수의 평균 값을 계산해 주는 함수를 작성해 보자. 
# (단 입력으로 들어오는 수의 개수는 정해져 있지 않다.)

def cal_median(*args):
  result = 0
  for i in args:
    result = result + i
  return result / len(args)

result = cal_median(1,2,3,4,5,6,7,8,9,10)
print(result)
```

    5.5
    


```python
# Q3 다음은 두 개의 숫자를 입력받아 더하여 돌려주는 프로그램이다.
# 3과 6을 입력했을 때 9가 아닌 36이라는 결괏값을 돌려주었다. 이 프로그램의 오류를 수정해 보자.

input1 = int(input("첫번째 숫자를 입력하세요:"))
input2 = int(input("두번째 숫자를 입력하세요:"))
# int를 통한 형변환을 시행.

total = input1 + input2
print("두 수의 합은 %s 입니다" % total)
```

    첫번째 숫자를 입력하세요:1
    두번째 숫자를 입력하세요:4
    두 수의 합은 5 입니다
    


```python
# Q4 다음 중 출력 결과가 다른 것 한 개를 골라 보자.

print("you" "need" "python")
print("you"+"need"+"python")
print("you", "need", "python")   #  콤마를 이요한 띄어쓰기를 사용함
print("".join(["you", "need", "python"]))
```

    youneedpython
    youneedpython
    you need python
    youneedpython
    


```python
# Q5 다음은 "test.txt"라는 파일에 "Life is too short" 문자열을 저장한 후 다시 그 파일을 읽어서 출력하는 프로그램이다. 
# 예상한 값을 출력할 수 있도록 프로그램을 수정해 보자.

f1 = open("test.txt", 'w')
f1.write("Life is too short")
f1.close() # 열린 파일 객체를 닫는다.

f2 = open("test.txt", 'r')
print(f2.read())
f2. close() # close를 추가함.
```

    Life is too short
    


```python
# Q6 사용자의 입력을 파일(test.txt)에 저장하는 프로그램을 작성해 보자. 
#(단 프로그램을 다시 실행하더라도 기존에 작성한 내용을 유지하고 새로 입력한 내용을 추가해야 한다.)
# 다시 풀어보자

user_input = input("저장할 내용을 입력하세요:")
f = open('test.txt', 'a')     # 내용을 추가하기 위해서 'a'를 사용
f.write(user_input)
f.write("\n")                 # 입력된 내용을 줄 단위로 구분하기 위한 개행 문자 사용
f.close()
```

    저장할 내용을 입력하세요:hihi
    


```python
# Q7 다음과 같은 내용을 지닌 파일 test.txt가 있다.  이 파일의 내용 중 "java"라는 문자열을 "python"으로 바꾸어서 저장해 보자.
# 다시 풀어보자
f = open('test.txt', 'r')
body = f.read()
f.close()

body = body.replace('java', 'python')

f = open('test.txt', 'w')
f.write(body)
f.close()
```
