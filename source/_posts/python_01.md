---
title: "파이썬_기초문법_1"
tags:
  - python
categories:
  - python
  - 기초문법
author: "minkuen"
date: '2022-03-22'
---

### Hello world


```python
print("Hello, World")
```

    Hello, World
    

# 주석 처리
- 코드 작업 시, 특정 코드에 대해 설명
- 사용자 정의 함수 작성 시, 클래스 작성시.. (도움말 작성..)


```python
# 한 줄 주석 처리
'''
여러 줄 주석 처리 시
'''

print( "Hello, World!")
```

    Hello, World!
    

# 변수 (Scalar)
- 객체(Object)로 구현이 됨
  + 하나의 자료형(Type)을 가진다.
  + 클래스로 정의가 됨.
    - 다양한 함수들이 존재 함.

## int
- init 정수를 표현하는데 사용함.


```python
#데이터 전처리..
#데이터 전처리를 잘해야! 분석도 잘함. 예측 모형도 잘 만듬.
#데이터 전처리를 잘하기 위해서는, 기초문법이 중요함.

num_int = 1
num_int2 = 3
print(num_int)
print(num_int2)
print(type(num_int))
```

    1
    3
    <class 'int'>
    

## float
- 실수를 표현하는데 사용한다.


```python
num_float = 0.2
print(num_float)
print(type(num_float))
```

    0.2
    <class 'float'>
    


```python
## bool
- True와 False로 나타내는 Boolean 값을 표현하는데 사용한다.
```


```python
bool_true = True
print(bool_true)
print(type(bool_true))
```

    True
    <class 'bool'>
    

## None
- Null을 나타내는 자료형으로 None이라는 한 가지 값만 가집니다.


```python
none_x = None
print(none_x)
print(type(none_x))
```

    None
    <class 'NoneType'>
    

# 사칙연산
- 정수형 사칙 연산



```python
a = 10
b = 5
print('a + b = ', a+b)
print('a - b = ', a-b)
print('a * b = ', a*b)
print('a / b = ', a/b)
print('a // b = ', a//b)
print('a % b = ', a%b)
print('a ** b = ', a**b)
```

    a + b =  15
    a - b =  5
    a * b =  50
    a / b =  2.0
    a // b =  2
    a % b =  0
    a ** b =  100000
    

# 실수형 사칙연산


```python
a = 10.0
b = 5.0
print('a + b = ', a+b)
print('a - b = ', a-b)
print('a * b = ', a*b)
print('a / b = ', a/b)
print('a // b = ', a//b)
print('a % b = ', a%b)
print('a ** b = ', a**b)
```

    a + b =  15.0
    a - b =  5.0
    a * b =  50.0
    a / b =  2.0
    a // b =  2.0
    a % b =  0.0
    a ** b =  100000.0
    

# 논리형 연산자
- Bool 형은 True와 False 값으로 정의
- AND / OR


```python
x = 5 > 4  # True
y = 3 > 4  # False

print(x and x)
print(x and y)
print(y and x)
print(y and y)
print("-----")
print(x or x)
print(x or y)
print(y or x)
print(y or y)
```

# 비교 연산자
- 부등호를 의미합니다.
- 비교 연산자를 True와 False값을 도출

# 논리 & 비교 연산자 응용


```python
var = input("입력해주세요....")
print(type(var))   # 숫자를 입력해도 str로 판단
```

    입력해주세요....1
    <class 'str'>
    

- 형변환을 해준다.
- 문자열, 정수, 실수 등등등


```python
var = int("1")   # 형변환
print(type(var))
```

    <class 'int'>
    


```python
var = int(input("숫자를 입력하여 주세요 : "))  # 형변환
print(type(var))
```

    숫자를 입력하여 주세요 : 1
    <class 'int'>
    


```python
num1 = int(input("숫자를 입력하여 주세요... : ")) # 10
num2 = int(input("숫자를 입력하여 주세요... : ")) # 3
num3 = int(input("숫자를 입력하여 주세요... : ")) # 5
num4 = int(input("숫자를 입력하여 주세요... : ")) # 7

var1 = num1 >= num2 # True
var2 = num3 < num4  # True
print(var1 and var2)
print(var1 or var2) 
```

    숫자를 입력하여 주세요... : 10
    숫자를 입력하여 주세요... : 3
    숫자를 입력하여 주세요... : 5
    숫자를 입력하여 주세요... : 7
    True
    True
    

# 변수 ( Non Scalar)
- 문자열을 입력



```python
print("'Hello, world'")
print('"Hello, world"')
```

    'Hello, world'
    "Hello, world"
    

## String 연산자
- 덧셈 연산자를 써보자.


```python
str1 = "Hello "
str2 = "World! "
str3 = "\n"
print(str1 + str2)
```

    Hello World! 
    

- 곱셈 연산자를 사용해본다.


```python
greeting = str1 + str2 + str3
print(greeting * 3)
```

    Hello World! 
    Hello World! 
    Hello World! 
    
    

# indexing
- 문자열 인덱싱은 각각의 문자열 안에서 범위를 지정하여 특정 문자를 추출한다.


```python
greeting = "Hello kaggle!"
print(greeting[6])
```

    k
    

# 슬라이싱
- 범위를 지정하고 데이터를 가져온다.


```python
greeting

print(greeting[:]) 
print(greeting[6:]) 
print(greeting[:6])  # 시작 인덱스 ~ 끝 인덱스-1 만큼 출력하므로 Hello
print(greeting[3:9])
print(greeting[0:9:2]) # 3번째 index는 몇번 건너띄는 것인지 표시 
```

    Hello kaggle!
    kaggle!
    Hello 
    lo kag
    Hlokg
    

# 리스트
- 시퀀스 데이터 타입
- 데이터에 순서가 존재하냐! 슬라이실이 가능해야 함.
- 대관호 (['값1', '값2', '값3'])



```python
a = []           # 빈 리스트
a_func = list()  # 빈 리스트 생성
b = [1]          # 숫자가 요소가 될 수 있다.
c = ['apple']    # 문자열도 요소가 될 수 있다.
d = [1, 2, ['apple']]  # 리스트 안에 또 다른 리스트 요소를 넣을 수 있다.

print(a)
print(a_func)
print(b)
print(c)
print(d)
```

    []
    []
    [1]
    ['apple']
    [1, 2, ['apple']]
    

# 리스트 슬라이싱


```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# print(a)
print(a[0])
print(a[6:])
print(a[:5])
print(a[3:5])
print(a[1:9:2])
```

    1
    [7, 8, 9, 10]
    [1, 2, 3, 4, 5]
    [4, 5]
    [2, 4, 6, 8]
    


```python
a = [["apple", "banana", "cherry"], 1]
print(a[0])
print(a[0][2])
print(a[0][0][4])
print(a[0][0][-1])
print(a[0][2][2])
```

    ['apple', 'banana', 'cherry']
    cherry
    e
    e
    e
    


```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(a[::-1])  # 역순
print(a[::2])
```

    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
    [1, 3, 5, 7, 9]
    


```python
## 리스트 연산자
a = ["john", "evan"]
b = ["alice", "eva"]

c = a + b
print(c)
```

    ['john', 'evan', 'alice', 'eva']
    


```python
c = a * 3
d = b * 0
print("a * 3 = ", c)
print("b * 0 = ", d)
```

    a * 3 =  ['john', 'evan', 'john', 'evan', 'john', 'evan']
    b * 0 =  []
    

## 리스트 수정 및 삭제


```python
a = [0, 1, 2]
a[1] = "b"
print(a)
```

    [0, 'b', 2]
    

### 리스트 값 추가하기


```python
a = [100, 200, 300]
a.append(400)
print(a)

a.append([500, 600])
print(a)
 
a.extend([500, 600])   # extend는 []없이 추가한다.
print(a)
```

    [100, 200, 300, 400]
    [100, 200, 300, 400, [500, 600]]
    [100, 200, 300, 400, [500, 600], 500, 600]
    


```python
a = [0, 1, 2]
# a.insert(인덱스번호, 넣고자하는 값)
a.insert(1,100)
print(a)
```

    [0, 100, 1, 2]
    

### 리스트 값 삭제하기


```python
a = [4, 3, 2, 1, "A"]
a.remove(1)  # 리스트 안에 있는 값을 삭제
print(a)
a.remove("A")
print(a)
```

    [4, 3, 2, 'A']
    [4, 3, 2]
    


```python
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

del a[1]  # 인덱스 번호
print(a)

del a[1:5]
print(a)
```

    [1, 3, 4, 5, 6, 7, 8, 9, 10]
    [1, 7, 8, 9, 10]
    


```python
b = ["a", "b", "c", "d"]
x = b.pop()  # 맨 끝자리 하나를 가져온다.
print(x)
print(b)
```

    d
    ['a', 'b', 'c']
    

### 그 외 메서드


```python
a = [0, 1, 2, 3]
print(a)

a.clear()
print(a)
```

    [0, 1, 2, 3]
    []
    


```python
a = ["a", "a", "b", "b"]
print(a.index("a"))  # 해당 문자가 여럿 있을 경우, 처음 하나만 출력
print(a.index("b")) 
```

    0
    2
    


```python
a = [1, 4, 5, 2, 3]
b = [1, 4, 5, 2, 3]

a.sort()
print("sort() : ", a)

# 내림차순 
b.sort(reverse=True)
print("sort(reverse=True) : ", b)
```

    sort() :  [1, 2, 3, 4, 5]
    sort(reverse=True) :  [5, 4, 3, 2, 1]
    

# 튜플
- List와 비슷하다.
- 슬라이싱, 인덱싱 등등
- (vs 리스트) : 튜플은 수정 삭제가 안된다.


```python
tuple1 = (0)  # 끝에 코마(,)를 붙이지 않을 때
tuple2 = (0, )  # 끝에 코마 붙일 때
tuple3 = 0, 1, 2
print(type(tuple1))
print(type(tuple2))
print(type(tuple3))
```

    <class 'int'>
    <class 'tuple'>
    <class 'tuple'>
    


```python
a = (0, 1, 2, 3, 'a')
print(type(a))

print(a)
b[1]="b"

a= tuple(b)
print(a)
```

    <class 'tuple'>
    (0, 1, 2, 3, 'a')
    (5, 'b', 3, 2, 1)
    

### 튜플 인덱싱 및 슬라이싱 하기


```python
a = (0, 1, 2, 3, 'a')
print(a[1])
print(a[2])
print(a[4])
```

    1
    2
    a
    

### 더하기 곱셈 연산자 사용


```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

print(t1 + t2)
print(t1 * 3)
print(t1 * 0)
```

    (1, 2, 3, 4, 5, 6)
    (1, 2, 3, 1, 2, 3, 1, 2, 3)
    ()
    

# 딕셔너리
- key & value 값으로 나뉨.


```python
dict_01 = {'teacher' : 'evan',
           'class' : 601,
           'students' : 24,
           '학생이름' : ['A', 'Z']}
dict_01
print(dict_01['teacher'])
print(dict_01['class'])
print(dict_01['학생이름'])
```

    evan
    601
    ['A', 'Z']
    


```python
print(dict_01.keys())

print(list(dict_01.keys()))
```

    dict_keys(['teacher', 'class', 'students', '학생이름'])
    ['teacher', 'class', 'students', '학생이름']
    


```python
print(dict_01.values())
```

    dict_values(['evan', 601, 24, ['A', 'Z']])
    


```python
dict_01.items()
```




    dict_items([('teacher', 'evan'), ('class', 601), ('students', 24), ('학생이름', ['A', 'Z'])])




```python
print(dict_01.get("teacher"))   # get 메소드
print(dict_01.get("선생님", "값 없음"))
print(dict_01.get("class"))
print(dict_01.get("students"))
```

    evan
    값 없음
    601
    24
    

#  조건문 & 반복분
- 일상에서 조건문 언제쓸까요?


```python
# 날씨가 맑다 --> 우산을 안 책겨간다
# 날씨가 흐리다 -> 우산을 챙긴다
weather = "맑음"
if weather == "비":
  print("우산을 가져간다")
else :
  print("우산을 가져가지 않는다")
```

    우산을 가져가지 않는다
    


```python
# 등급표 만들기
# 60점 이상 합격 / 불합격
# 숫자는 아무거나 써도 상관없음

grade = 70
if grade > 60 :
  print("합격입니다.")
else :
  print("불합격입니다.")
```

    합격입니다.
    


```python
grade = int(input("숫자를 입력하여 주세요... : "))
if grade > 60 :
  print("합격입니다.")
else :
  print("불합격입니다.")
```

    숫자를 입력하여 주세요... : 10
    불합격입니다.
    


```python
# 90점 이상은 A등급
# 80점 이상은 B등급
# 나머지는 F등급
grade = int(input("숫자를 입력하여 주세요... : "))
if grade >= 90 :
  print("A 등급입니다.")
elif grade >= 80 :
  print("B 등급입니다.")
else :
  print("F 등급입니다.")
```

    숫자를 입력하여 주세요... : 85
    B 등급입니다.
    

### 반복문


### for문


```python
# 안녕하세요! 5번 반복하라
for i in range(5) : 
  print(i+1, "안녕하세요")
```

    1 안녕하세요
    2 안녕하세요
    3 안녕하세요
    4 안녕하세요
    5 안녕하세요
    


```python
count = range(5)
print(count)

for n in count:
  print(str(n+1) + "번째")
  if(n+1) == 3:
    print("그만합니다")
    break
  print("축구 슈팅")

```

    range(0, 5)
    1번째
    축구 슈팅
    2번째
    축구 슈팅
    3번째
    그만합니다
    


```python
a = "hello"
for x in a :
  if x in a :
    if x == "l" :
      break
    print(x)
```

    h
    e
    

### while문
반복해서 문장을 수행해야 할 경우 while문을 사용한다.


```python
#열 번 찍어 안 넘어가는 나무 없다"
treehit = 0
while treehit < 10:
  treehit = treehit + 1
  print("나무를 %d번 찍었습니다." % treehit)
  if treehit == 10:
    print("나무가 넘어갑니다.")
```

    나무를 1번 찍었습니다.
    나무를 2번 찍었습니다.
    나무를 3번 찍었습니다.
    나무를 4번 찍었습니다.
    나무를 5번 찍었습니다.
    나무를 6번 찍었습니다.
    나무를 7번 찍었습니다.
    나무를 8번 찍었습니다.
    나무를 9번 찍었습니다.
    나무를 10번 찍었습니다.
    나무 넘어갑니다.
    


```python
# while문 만들기
prompt = """
1.Add
2.Del
3.List
4.Quit
Enter number: """
```


```python
number = 0
while number != 4:
  print(prompt)
  number = int(input())
```

    
    1.Add
    2.Del
    3.List
    4.Quit
    Enter number: 
    4
    


```python
# 커피 자판기 이야기
coffee = 10
money = 300
while money :
  print("돈을 받았으니 커피를 줍니다.")
  coffee = coffee - 1
  print("남은 커피의 양은 %d개입니다." % coffee)
  if coffee == 0:
    print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
    break
```

### while문의 맨 처음으로 돌아가기 (continue)


```python
a = 0
while a < 10 :
  a = a + 1
  if a % 2 == 0 :
    continue
  print(a)
```

    1
    3
    5
    7
    9
    

### 무한 루프


```python
while True :
  print("Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.")
```

# 문자열 포매팅
-  문자열 안의 특정한 값을 바꿔야 할 경우가 있을 때 이것을 가능하게 해주는 것이 바로 문자열 포매팅 기법이다.
- 숫자는 %d, 문자는 %s 



```python
# 숫자 바로 대입 
"I eat %d apple." % 3
```




    'I eat 3 apple.'




```python
# 문자열 바로 대입
"I eat %s apples." % "five"
```




    'I eat five apples.'




```python
# 숫자 값을 나타내는 변수로 대입
number = 3
"I eat %d apples." % number
```




    'I eat 3 apples.'




```python
# 2개 이상의 값 넣기
number = 10
day = "three"
"I ate %d apples. so I was sick for %s day" % (number, day)
```




    'I ate 10 apples. so I was sick for three day'




```python
"I have %s apples" % 3
"rate is %s " % 3.234
```




    'rate is 3.234 '



# format 함수를 사용한 포매팅 
- 문자열의 format 함수를 사용하면 좀 더 발전된 스타일로 문자열 포맷을 지정할 수 있다. 


```python
# 숫자 바로 대입하기
"I eat {0} apples".format(3)
```




    'I eat 3 apples'




```python
# 문자 바로 대입하기
"I eat {0} apples".format("five")
```




    'I eat five apples'




```python
# 숫자 값을 가진 변수로 대입하기
number = 3
"I eat {0} apples".format(number)
```




    'I eat 3 apples'




```python
# 2개 이상의 값 넣기
number = 10
day = "three"
"I ate {0} apples. so I was sick for {1} days. ".format(number, day)
```




    'I ate 10 apples. so I was sick for three days. '




```python
# 이름으로 넣기
"I ate {number} apples. so I was sick for {day} days.".format(number=10, day=3)
```




    'I ate 10 apples. so I was sick for 3 days.'




```python
# 인덱스와 이름을 혼용해서 넣기
"I ate {0} apples. so I was sick for {day} days.".format(10, day=3)
```




    'I ate 10 apples. so I was sick for 3 days.'




```python
# 왼쪽 정렬
"{0:<10}".format("hi")   # 왼쪽으로 정렬하고 총 자릿수를 10으로 설정.
```




    'hi        '




```python
# 오른쪽 정렬
"{0:>10}".format("hi")   # 오른쪽으로 정렬하고 총 자릿수를 10으로 설정.
```




    '        hi'




```python
# 가운데 정렬
"{0:^10}".format("hi")
```




    '    hi    '




```python
# 공백 채우기
"{0:=^10}".format("hi")
"{0:!<10}".format("hi")
```




    'hi!!!!!!!!'




```python
# 소수점 표현하기
y = 3.42134234
"{0:0.4f}".format(y)   # 소수점을 4자리까지만 표현
```




    '3.4213'




```python
# 정렬과 소수점 표현 
"{0:10.4f}".format(y)
```




    '    3.4213'




```python
# { 또는 } 문자 표현하기
"{{ and }}".format()
```




    '{ and }'



# f 문자열 포매팅
- 파이썬 3.6 버전부터는 f 문자열 포매팅 기능을 사용할 수 있다.
-  f 문자열 포매팅은 표현식을 지원한다.
-  표현식이란 문자열 안에서 변수와 +, -와 같은 수식을 함께 사용하는 것을 말한다.




```python
name = '홍길동'
age = 30
f'나의 이름은 {name}입니다. 나이는 {age}입니다.'
```




    '나의 이름은 홍길동입니다. 나이는 30입니다.'




```python
age = 30
f'나는 내년이면 {age+1}살이 된다.'
```




    '나는 내년이면 31살이 된다.'




```python
# f 문자열 포매팅에서의 딕셔너리
d = {'name':'홍길동', 'age':30}
f'나의 이름은 {d["name"]}입니다. 나이는 {d["age"]}입니다.'
```




    '나의 이름은 홍길동입니다. 나이는 30입니다.'




```python
# f 문자열에서 정렬
f'{"hi":<10}'
f'{"hi":>10}'
f'{"hi":^10}'
```




    '    hi    '




```python
# f 문자열에서 공백채우기
f'{"hi":=^10}'
f'{"hi":!<10}'
```




    'hi!!!!!!!!'




```python
# f 문자열에서 소수점표현
y = 3.42134234
f'{y:0.4f}'
f'{y:10.4f}'
```




    '    3.4213'




```python
# f 문자열에서 { } 문자를 표시
f'{{ and }}'
```




    '{ and }'



# 문자열 관련 함수들
- 문자열 자료형은 자체적으로 함수를 가지고 있다.
- 이들 함수를 다른 말로 문자열 내장 함수라 한다.
- 이 내장 함수를 사용하려면 문자열 변수 이름 뒤에 ‘.’를 붙인 다음에 함수 이름을 써주면 된다.


```python
# 문자 개수 세기 (count)
a = "hobby"
a.count('b')
```




    2




```python
# 위치 알려주기1 (find)
a = "Python is the best choice"
a.find('b')
a.find('k')   # 찾는 문자가 없다면 -1을 반환.
```




    -1




```python
# 위치 알려주기2 (index)
a = "Life is too short"
a.index('t')
```




    8



### 문자열 삽입(join)


```python
",".join('abcd')
```




    'a,b,c,d'




```python
# 대문자를 소문자로 바꾸기
a = "HI"
a.lower()
```




    'hi'




```python
# 왼쪽 공백 지우기
a = "  hi  "
a.lstrip()
```




    'hi  '




```python
# 오른쪽 공백 지우기(rstrip)
a = "  hi  "
a.rstrip()
```




    '  hi'




```python
# 양쪽 공백 지우기(strip)
a = "  hi  "
a.strip()
```




    'hi'



### 문자열 바꾸기(replace)


```python
a = "Life is too short"
a.replace("Life", "your leg")
```




    'your leg is too short'



### 문자열 나누기(split)


```python
a = "Life is too short"
a.split()

b = "a:b:c:d"
b.split(':')
```




    ['a', 'b', 'c', 'd']




```python
# 
```



# 2장 연습문제
- 파이썬 프로그래밍의 기초, 자료형


```python
# Q1 홍길동 씨의 과목별 점수는 다음과 같다. 홍길동 씨의 평균 점수를 구해 보자.
from IPython.core.display import Math

kor = 80
en = 75
math = 55

mean = (kor + en + math) / 3
print(mean)
```

    70.0
    


```python
# Q2 자연수 13이 홀수인지 짝수인지 판별할 수 있는 방법에 대해 말해 보자..
from IPython.core.display import Math

if 13 % 2 == 1 :
  print("13은 홀수이다")
else :
  print("13은 짝수이다")
```

    13은 홀수이다
    


```python
# Q3 자연수 13이 홀수인지 짝수인지 판별할 수 있는 방법에 대해 말해 보자..

num = "881120-1068234"
num1 = num[:6]
num2 = num[7:]

print(num1)  
print(num2)
```

    881120
    1068234
    


```python
#Q4 주민등록번호에서 성별을 나타내는 숫자를 출력해 보자.

pin = "881120-1068234"
print(pin[7])
```

    1
    


```python
#Q5 다음과 같은 문자열 a:b:c:d가 있다.
#   문자열의 replace 함수를 사용하여 a#b#c#d로 바꿔서 출력해 보자.

a = "a:b:c:d"
a.replace(":", "#")
print(a)
```

    a:b:c:d
    


```python
#Q6 [1, 3, 5, 4, 2] 리스트를 [5, 4, 3, 2, 1]로 만들어 보자.
a = [1,3,5,4,2]
a.sort(reverse=True)
print(a)
```

    [5, 4, 3, 2, 1]
    


```python
#Q7 ['Life', 'is', 'too', 'short'] 리스트를 Life is too short 문자열로 만들어 출력해 보자.

a = ['Life', 'is', 'too', 'short']
print(a[0] + " " + a[1] + " " + a[2] + " " + a[3])
```

    Life is too short
    


```python
#Q8 (1,2,3) 튜플에 값 4를 추가하여 (1,2,3,4)를 만들어 출력해 보자.

t1 = (1, 2, 3)
t2 = (4, )
t1 + t2
```




    (1, 2, 3, 4)



Q9 다음과 같은 딕셔너리 a가 있다.

>>> a = dict()
>>> a
{}
다음 중 오류가 발생하는 경우를 고르고, 그 이유를 설명해 보자.
1.a['name'] = 'python'
2.a[('a',)] = 'python'
3.a[[1]] = 'python'
4.a[250] = 'python'


```python
#Q9 1번과 3번에서 오류가 발생합니다.
# 1번은 invalid syntax 오류
# 3번은 unhashable type: 'list' 오류
a = dict()
a
# a['name' = 'python']
a[('a',)] = 'python'
# a[[1]] = 'python'
a[250] = 'python'
```


```python
#Q10 딕셔너리 a에서 'B'에 해당되는 값을 추출해 보자.
dict_00 = {'A':90, 'B':80, 'C':70}
d = dict_00.pop('B')
print(dict_00)
print(d)
```

    {'A': 90, 'C': 70}
    80
    


```python
#Q11 a 리스트에서 중복 숫자를 제거해 보자.
# 다시 풀어보자
a = [1, 1, 1, 2, 2, 3, 3, 3, 4, 4, 5]
aset = set(a)
b = list(aset)
print(b)
```

    [1, 2, 3, 4, 5]
    

Q12 파이썬은 다음처럼 동일한 값에 여러 개의 변수를 선언할 수 있다. 다음과 같이 a, b 변수를 선언한 후 a의 두 번째 요솟값을 변경하면 b 값은 어떻게 될까? 그리고 이런 결과가 오는 이유에 대해 설명해 보자.
a = b = [1, 2, 3]
a[1] = 4
print(b)


```python
#Q12 
a = b = [1,2,3]
a[1] = 4
print(b)
#  a=b 라고 설정했기 때문에 다음 결과가 나옵니다.
```

    [1, 4, 3]
    

# 3장 연습문제


```python
#Q1 다음 코드의 결괏값은?
a = "Life is too short, you need python"

if "wife" in a : print("wife")
elif "python" in a and "you" not in a : print("python")
elif "shirt" not in a : print("shirt")
elif "need" in a : print("need")
else: print("none")
```

    shirt
    


```python
#Q2 while문을 사용해 1부터 1000까지의 자연수 중 3의 배수의 합을 구해 보자.
count = 1
sum = 0
while count < 1000 :
  count = count + 1
  if count % 3 == 0 :
    sum = sum + count

print(sum)
```

    166833
    


```python
#Q3 while문을 사용하여 다음과 같이 별(*)을 표시하는 프로그램을 작성해 보자.
count = 0
while count < 5:
  count = count + 1
  print("*" * count) 
```

    *
    **
    ***
    ****
    *****
    


```python
#Q4 for문을 사용해 1부터 100까지의 숫자를 출력해 보자.
for num in range(100):
  print(num+1)
```


```python
#Q5 A 학급에 총 10명의 학생이 있다. 이 학생들의 중간고사 점수는 다음과 같다.
#[70, 60, 55, 75, 95, 90, 80, 80, 85, 100]
#for문을 사용하여 A 학급의 평균 점수를 구해 보자.
sum = 0
a_class = [70, 60, 55, 75, 95, 90, 80, 80, 85, 100]
for num in a_class :
  sum = sum + num

mean = sum / len(a_class)
print(mean)
```

    79.0
    


```python
#Q6 리스트 중에서 홀수에만 2를 곱하여 저장하는 다음 코드가 있다. 

numbers = [1, 2, 3, 4, 5]
result = []
for n in numbers:
    if n % 2 == 1:
        result.append(n*2)
        
# 위 코드를 리스트 내포(list comprehension)를 사용하여 표현해 보자.
# 다시 풀어보자
numbers = [1, 2, 3, 4, 5]
result = [n*2 for n in numbers if n%2==1]
print(result)
```

    [2, 6, 10]
    
