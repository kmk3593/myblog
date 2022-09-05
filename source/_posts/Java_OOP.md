---
title: "JAVA OOP"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-07-20'
---

# 객체 지향 - class

### 클래스

- class는 객체에 대한 설계도
- 설계도 대로 인스턴스를 하나 만들면 그제서야 메모리에 올라간다

### 사용법

- 객체를 사용해보자.
- 어떻게?
    1. 서로 다른 클래스에 함수를 만든다
    2. main에서 사용할 클래스의 함수를 new로 선언한다. **(생성자 이용 가능)**
    3. new로 선언한 클래스의 변수나 함수를 호출하여 사용

**생성자 Constructor객체**

- 역할 : 객체를 인스턴스화(생성) 하는 역할
- 문법 : 함수와 비슷하게 생겼는데 이름이 클래스명이고 리턴 값이 없다

- 객체를 생성할 때 new 키워드와 함께 사용. **생성할 때 필요한 데이터를 강제**하는 역할
- 클래스에는 반드시 최소하나이상의 생성자가 존재
- 클래스에 생성자가 명시적으로 없더라도 컴파일러가 디폴트 생성자를 넣어주기 때문에 new키워드와 함께 생성자를 호출 가능하다
- 디폴트 생성자는 매개변수와 구현부가 없다

### 실습

- Human 클래스를 만든다
- 객체로서 필요한 정보(이름,나이 등)를 설정
- 객체로서 행동(달리기, 동물 기르기 등)을 설정
- Human.java

```java
public class Human {
//	이름, 나이, 성별
//	길들이다, 먹이를 주다, 달리다
	
	String name = "김씨";
	int age = 20;
	String gender = "male";
	
	public void taming(Dog animal) {
		System.out.println(this.name + "이(가) " + animal.name+"을(를) 길들이겠습니다.");
	}
	public void feed() {
		System.out.println("동물에게 먹이를 주다");
	}
	public void run() {
		System.out.println("달려나가다");
	}
}
```

- Dog 클래스를 만든다
- 객체로서 필요한 정보(이름, 나이 등)를 설정
- 객체로서 행동(달리기, 점프하기 등)을 설정
- Dog.java

```java
public class Dog {
//	털색, 키, 몸무게, 품종, 나이, 걷기, 뛰기, 점프하기,
//	구르기, 활퀴기, 자기, 먹기, 울음소리
	String name = "멍멍이";
	String color = "갈색";
	double weight = 15.3;
	String kind = "달마시안";
	int age = 5;

	public void walk() {
		System.out.println("걷습니다.");
	}
	public void run() {
		System.out.println("달립니다.");
	}
	public void jump() {
		System.out.println("점프합니다.");
	}
}
```

- Main에서 의도대로 작성한 클래스들을 이용해본다
- main.java

```java
public class Main {

	public static void main(String[] args) {

		Dog mydog1 = new Dog();           // Dog클래스에서 mydog1 객체 생성
		System.out.println(mydog1.name);  // mydog1 이름 출력
		
		Human kim = new Human();          // Human클래스에서 kim 객체 생성
		kim.taming(mydog1);               // kim이 mydog1을 인자로 받아서 함수 싱행 
	}
}
```

- 결과
- [main.java](http://main.java) 클래스를 실행한 결과이다.

![Untitled](/images/Java_OOP/Untitled.png)

### 생성자 사용 vs 비사용

- 생성자 = 객체를 생성할 때 new 키워드와 함께 사용. **생성할때 필요한 데이터를 강제**하는 역할.

[**생성자 비사용]**

- 특징 : 미리 변수의 내용을 설정해야 한다
- Human.java
    
    ```java
    public class Human {
    //	이름, 나이, 성별
    //	길들이다, 먹이를 주다, 달리다
    	String name="김씨";
    	int age=10;
    	String gender="male";
    	
    	public void walk() {
    		System.out.println("여유롭게 걸어갑니다");
    	}
    	public void run() {
    		System.out.println("신속하게 달려나갑니다");
    	}
    }
    ```
    
- Main.java
    
    ```java
    public class Main {
    
    	public static void main(String[] args) {
    
    		Human kim = new Human();       // Human 클래스에서 kim 객체 생성
    		System.out.println(kim.name);  // kim 이름 출력
    		kim.walk();                    // kim의 함수 호출
    		
    //		Dog dog1 = new Dog();          // Dog 클래스에서 dog1 객체 생성
    //		dog1.jump();				   // dog1의 함수 호출
    		
    	}
    }
    ```
    

![Untitled](/images/Java_OOP/Untitled%201.png)

[**생성자 사용]**

- 특징 : **미리 변수의 내용을 설정하지 않아도  작동**한다
- 단, **생성할때 필요한 데이터 입력를 강제**한다
- 생성자 쉽게 생성 = ctrl + space바 + Enter
- Human.java
    
    ```java
    public class Human {
    //	이름, 나이, 성별
    //	길들이다, 먹이를 주다, 달리다
    	String name;
    	int age;
    	String gender;
    	
    	public Human(String name, int age) {
    		this.name = name;
    		this.age = age;
    	
    	}
    	public void walk() {
    		System.out.println("여유롭게 걸어갑니다");
    	}
    	public void run() {
    		System.out.println("신속하게 달려나갑니다");
    	}
    }
    ```
    
- Main.java
    
    ```java
    public class Main {
    
    	public static void main(String[] args) {
    
    		Human kim = new Human("아무개", 21);       // Human 클래스에서 kim 객체 생성
    		System.out.println(kim.name);  // kim 이름 출력
    		kim.walk();                    // kim의 함수 호출
    		
    //		Dog dog1 = new Dog();          // Dog 클래스에서 dog1 객체 생성
    //		dog1.jump();				   // dog1의 함수 호출
    		
    	}
    }
    ```
    

![Untitled](/images/Java_OOP/Untitled%202.png)

### 개인 실습

- 이후에 개인적으로 클래스를 사용해보자
- 간단한 게임 제작
- 위에서 한 것처럼 플레이어 클래스, 몬스터 클래스를 생성
- 서로에게 공격하는 함수를 넣고 main에서 사용해보자