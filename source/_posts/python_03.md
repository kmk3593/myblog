---
title: "파이썬_기초문법_3"
tags:
  - python
categories:
  - python
  - 기초문법
  - 클래스
author: "minkuen"
date: '2022-03-23'
---

# 클래스를 만드는 목적!
- 코드의 간결화!
  + 코드를 재사용!
- 여러 라이브러리 --> 클래스로 구현이 됨
  + list 클래스, str 클래스
  + 객체로 사용
  + 변수명으로 정의!
- 여러 클래스들이 모여서 하나의 라이브러리가 됨.
  + 장고 / 웹개발 / 머신러닝 / 시각화 / 데이터 전처리


```python
class Person:     # 클래스 이름 첫문자는 대문자로 설정

  #class attribute
  country = "korean"

  #instance attribute         
  def __init__(self, name, age):    # def __init__(self, ) 는 디폴트로 정해진 부분이다
    self.name = name
    self.age = age

if __name__ == "__main__":
  kim = Person("Kim", 100)
  Lee = Person("lee", 100)

  # access class attribute
  print("kim은 {}".format(kim.__class__.country))
  print("Lee는 {}".format(Lee.__class__.country))
```

    kim은 korean
    Lee은 korean
    

## instance 메서드 생성
- list.append(), list.extend()


```python
class Person:     

  
  country = "korean"

    
  def __init__(self, name, age):    
    self.name = name
    self.age = age

  # instance method 정의
  def singing(self, songtitle, sales):
    return "{}판매량 {}된 {}을 노래합니다.".format(self.name, sales, songtitle)

if __name__ == "__main__":
  kim = Person("Kim", 100)
  Lee = Person("lee", 100)

  # access class attribute
  print("kim은 {}".format(kim.country))
  print("Lee는 {}".format(Lee.__class__.country))

  # call instance method
  print(kim.singing("A", 10))
  print(Lee.singing("B", 200))
```

    kim은 korean
    Lee는 korean
    Kim판매량 10된 A을 노래합니다.
    lee판매량 200된 B을 노래합니다.
    


```python
name = "lee"
songtitle = "B"
print("{} {}을 노래합니다.".format(name, songtitle))
```

    lee B을 노래합니다.
    

## 클래스 상속
- 부모님 유산...
  + 부모님 집 (냉장고, 세탁기, TV, etc)
  + 사용은 같이 함
- 본인, 돈을 모음
  + 개인 노트북 구매 ( 여러분 각자 방에 비치 )
  + 노트분은 본인 것이지만 추가 가전 제품을 구매해서 확장!


```python
class Parent:
  pass
class Child(Parent):
  pass
if __name__ == "__main__":
  kim_child = Child()
```


```python
class Parent:

  # instance attribute
  def __init__(self, name, age):    
    self.name = name
    self.age = age

  def whoAmI(self):
    print("I am Parent!!")

  def singing(self, songtitle):
    return "{}된 {}을 노래합니다.".format(self.name, songtitle)

  def dancing(self):
    return "{} 현재 춤을 춥니다.".format(self.name)

class Child(Parent):              # 상속
  def __init__(self, name, age):
    #super() function             # 상속 기능
    super().__init__(name, age)
    print("Child Class is ON")

  def whoAmI(self):
    print("I am child")
  
  def studying(self):
    print("I am Fast Runner")

if __name__ == "__main__":
  child_kim = Child("kim", 15)
  parent_kim = Parent("kim", 45)
  print(child_kim.dancing())
  print(child_kim.singing("연애"))
 # print(child_kim.studying())
  child_kim.whoAmI()
  parent_kim.whoAmI()
```

    Child Class is ON
    kim 현재 춤을 춥니다.
    kim된 연애을 노래합니다.
    I am Fast Runner
    None
    I am child
    I am Parent!!
    


```python
class TV:

  #init constructor  ( 생성자 )
  def __init__(self):
    self.__maxprice = 500  # 클래스 내부에서 쓸 수 있게끔 private variable
  
  def sell(self):
    print("selling Price : {}".format(self.__maxprice))
  
  def setMaxPrice(self, price):
    self.__maxprice = price

if __name__ == "__main__":
  tv = TV()
  tv.sell()

  # change price
  # 안 바뀌는 코드의 예시
  tv.__maxprice = 1000
  tv.sell()

  # setMaxPrice
  # 값을 바꿀 수 있다?? 외부의 입력값을 업데이트 할 수 있다.
  tv.setMaxPrice(1000)
  tv.sell()
```

    selling Price : 500
    selling Price : 500
    selling Price : 1000
    

자식 클래스가 많이 있는 라이브러리는 사용자가 스기 까다로울 것 같은데, 많이 써주는 이유는 자식클래스 이름마다 의미를 주려고 그런건가요?
- 특수 목적을 해결하기 위해서 라이브러리를 만듦
- 초기 버전은 3개 클래스 정도 만들면 해결이 되겠지?
  + 버그 나오고, 이슈 터지고 --> 개발자들이 해결
- 2개 더 만들고 다시 배포
  +

## 클래스 내부에 조건문
- init contsructor에 조건문을 써보자!


```python
class Employee:

  #init constructor
  #name, salary
  def __init__(self, name, salary = 0):    
    self.name = name
    
    #조건문 추가
    if salary > 0:
      self.salary = salary
    else:
      self.salary = 0
      print("급여는 0원이 될 수 없습니다. 다시 입력해십시오!!")
    
  def update_salary(self, amount):
    self.salary += amount
  
  def weekly_salary(self):
    return self.salary / 7

if __name__ == "__main__":
  emp01 = Employee("Evan", -5000)
  print(emp01.name)
  print(emp01.salary)

  emp01.salary = emp01.salary + 1500
  print(emp01.salary)

  emp01.update_salary(3000)
  print(emp01.salary)

  week_salary = emp01.weekly_salary()
  print(week_salary)
```

    급여는 0원이 될 수 없습니다. 다시 입력해십시오!!
    Evan
    0
    1500
    4500
    642.8571428571429
    

### 클래스 Doctring
- 문서화
- 문서화의 일반적인 과정


```python
class Person:
  """
  사람을 표현하는 클래스
  ...

  Attributes
  ----------
  name : str
    name of the person
  
  age : int
    age of the person
  ...
  ...

  Methods
  ----------

  info(additional=""):
    prints the person's name and age
  """
  def __init__(self, name, age):
    """
    Constructs all the neccessary attributes for the person object

    Parameters
    ----------
    name : str
      name of the person
  
    age : int
      age of the person
    """

    self.name = name
    self.age = age

  def info(self, additional=None):
    """
    귀찮음...

    Parameters
    ----------
      additional : str, optional
        more info to be displayed (Default is None)

    Returns
    -------
      None
    """

    print(f'My name is {self.name}. i am {self.age} years old.' + additional)

  if __name__ == "__main__":
    person = Person("Evan", age = 20)
    person.info("나의 직장은 00이야")
    help(Person)
```

    My name is Evan. i am 20 years old.나의 직장은 00이야
    Help on class Person in module __main__:
    
    class Person(builtins.object)
     |  Person(name, age)
     |  
     |  사람을 표현하는 클래스
     |  ...
     |  
     |  Attributes
     |  ----------
     |  name : str
     |    name of the person
     |  
     |  age : int
     |    age of the person
     |  ...
     |  ...
     |  
     |  Methods
     |  ----------
     |  
     |  info(additional=""):
     |    prints the person's name and age
     |  
     |  Methods defined here:
     |  
     |  __init__(self, name, age)
     |      Constructs all the neccessary attributes for the person object
     |      
     |      Parameters
     |      ----------
     |      name : str
     |        name of the person
     |      
     |      age : int
     |        age of the person
     |  
     |  info(self, additional=None)
     |      귀찮음...
     |      
     |      Parameters
     |      ----------
     |        additional : str, optional
     |          more info to be displayed (Default is None)
     |      
     |      Returns
     |      -------
     |        None
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  person = <__main__.Person object>
    
    

# 클래스 실습


```python
# 더하기, 빼기 기능이 있는 클래스
class Calculator:
  def __init__(self):
    self.result = 0
  
  def add(self,num):
    self.result += num
    return self.result
  
  def sub(self,num):
    self.result -= num
    return self.result

cal1 = Calculator()
cal2 = Calculator()

print(cal1.add(3))
print(cal1.add(4))
print(cal2.add(3))
print(cal2.add(7))
```

    3
    7
    3
    10
    


```python
# 4칙연산 기능이 달린 클래스 정의
# 일단 더하기만 구현
class FourCal:
  def setdata(self, first, second):
    self.first = first
    self.second = second
  def add(self):
    result = self.first + self.second
    return result

a = FourCal()
a.setdata(4,2)
a.add()
```




    6




```python
# 4칙연산 기능이 달린 클래스 정의
class FourCal:
  def setdata(self, first, second):
    self.first = first
    self.second = second
  def add(self):
    result = self.first + self.second
    return result
  def mul(self):
    result = self.first * self.second
    return result
  def sub(self):
    result = self.first - self.second
    return result
  def div(self):
    result = self.first / self.second
    return result

a = FourCal()
a.setdata(4,2)

print(a.mul())
print(a.sub())
print(a.div())
```

    8
    2
    2.0
    

### 생성자
- 위 함수의 setdata는 생성자의 역할을 한다.
- setdata를 생성자 __init__으로 바꿔도 정상 작동한다.


```python
# setdata를 생성자 __init__으로 변경
class FourCal:
  def __init__(self, first, second):
    self.first = first
    self.second = second
  def add(self):
    result = self.first + self.second
    return result
  def mul(self):
    result = self.first * self.second
    return result
  def sub(self):
    result = self.first - self.second
    return result
  def div(self):
    result = self.first / self.second
    return result

a = FourCal(4, 2) # 이전과 달리 매개변수도 작성해야 작동.
print(a.mul())
print(a.sub())
print(a.div())
```

    8
    2
    2.0
    

### 클래스의 상속
-  FourCal 클래스는 만들어 놓았으므로 FourCal 클래스를 상속하는 MoreFourCal 클래스는 다음과 같이 간단하게 만들 수 있다.


```python
# 상속
class MoreFourCal(FourCal):
  pass

a = MoreFourCal(4,2)
a.add()
```




    6


