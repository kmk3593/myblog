---
title: "JAVA start"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-07-08'
---

### 코드 작성 팁

- System.out.println() 쉽게 작성하기
    - `Syso` + ctrl + space 바
- 한줄 복사
    - ctrl + alt + 아래방향키

### Hello World

- Spring Tool Suite4 실행
- 프로젝트 생성
- 우클릭 : 생성한 프로젝트의 src → New → class

![Untitled](/images/java_start_01/Untitled.png)

- Main 이라고 명명

![Untitled](/images/java_start_01/Untitled%201.png)

- 코드 작성
    - 팁 :  ctrl + space바

```html
package variable;

public class Main {
	public static void main(String[] args) {
		System.out.println("헬로 월드");
	}
	
}
```

- 저장 후 실행 결과

![Untitled](/images/java_start_01/Untitled%202.png)

- 여러가지 코드를 작성해보자

```html
package variable;

public class Main {
	public static void main(String[] args) {
//		System.out.println("헬로 월드");
		
		int a = 5;
		double b = 5.5;

		System.out.println(a+b);
		
		char x = 'a';
		String y = "hello";
		System.out.println(x+y);
		
		int myNum = a;
		myNum = myNum + 10;
		System.out.println("Mynum : " + myNum);
		System.out.println("a : " + a);
		
		Integer myInt = 5;
		Integer bInt = 9;
		myInt = bInt;	// 9

		myInt += 5;		// 14
		bInt += 10;		// 19
		System.out.println("myInt : "+myInt);
		System.out.println("bInt : "+bInt);
	}
}
```

### call by value, call by reference

- Main.java
- call by value = 값에 의한 참조
- call by reference = 주소에 의한 참조

```html
package variable;

public class Main {
	public static void main(String[] args) {
//		System.out.println("헬로 월드");
		
		int a = 5;
		double b = 7.5;

		System.out.println(a+b);
		
		// call by value. 기본형. 값에 의한 참조
		char x = 'a';
		String y = "hello";
		System.out.println(x+y);
		
		int myNum = a;
		myNum = myNum + 10;
		System.out.println("Mynum : " + myNum);
		System.out.println("a : " + a);
		
		// call by reference. 참조형. 주소에 의한 참조
		String[] imgArr = {"🍕", "🍖"};
		String[] stringArr = {"피자", "통닭", ""};
		imgArr = stringArr;	// 한글이 들어감
		stringArr[2] = "아이스크림";
		
		int i=0;
		System.out.println(imgArr[0]);
		System.out.println(imgArr[1]);
		System.out.println(imgArr[2]);
		
//		for(i=0; i<imgArr.length; i++) {
//			System.out.println(imgArr[i]);		
//		}
	}
}
```

### 연산자

```html
package variable;

public class 연산자 {
	public static void main(String[] args) {
	
		int a = 100;
		int b = 333;
		
		System.out.println(a++ + ++b); // 100 + 334 = 434
		// ++ 이나 -- 증감연산자가
		// 뒤에있으면 사용한뒤 값을 변경
		// 앞에 있으면 변경한 뒤에 사용
		
	}
}
```