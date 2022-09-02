---
title: "JAVA exception"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-08-27'
---

# Java_0617

### 학습목표

(클래스, 인스턴스, 오버로드, 함수정의, 함수호출, 데이터타입)

- 에러 : 개발자가 처리할 수 없는 심각한 영역의 문제. 반드시 프로그램이 종료되는 문제.
    - 문법에러 : 컴파일 전에 걸러지는 에러

- 예외 : 개발자가 프로그램을 죽이지 않고 대처할 수 있는 문제
    - 런탄임에 발생 : 컴파일은 통과했으나 실제 실행하니 발생하는 에러
    - 모든 예외는 자바의 Exception이라는 클래스를 상속받는다.
    
    예) Nullpointer, OutOfIndex, Arithmetic, ClassNotFound
    

### 예외

- 에러보다 덜 치명적인 비정상 상황
- 모든 예외클래스 는 java.lang.Exception 클래스를 상속받는다.
- 예외처리를 하게되면 프로그램이 종료되지 않고 계속 정상상태를 유지할 수 있다.
  < 예외처리 하는 법>
- 간단 : try, catch, finally 문법
- 구체적 : 

```java
try{
	예외가 발생할 가능성이 있는 코드
}catch(예외클래스 변수명){
   처리할 내용
}finally{
   예외가 있든 없든 처리할 내용
}
```

- 연습코드
- catch 문법 사용한 함수
    
    ```java
    public void printOneElement(int index) {
    		// 예외처리하고 정상범위 알려주기
    		try {
    			System.out.println(arr[index]);
    		} catch (Exception e){
    			e.printStackTrace(); // 어떤 예외가 발생했는지 로그를 출력
    			
    			System.out.println("해당위치는 범위를 넘어섰습니다. "+arr.length+"까지 허용범위입니다.");
    		} finally {
    			System.out.println("finally 실행");
    		}
    		
    		System.out.println("printOneElement 끝");
    	}
    ```
    
- 사용 결과
- 에러가 있음에도 이후의 코드가 실행되었다

![Untitled](/images/try_catch/Untitled.png)

### 인터페이스

- 구현체 implements 인터페이스.
- 부품들의 결합 방식에 대한 ""약속"". 다형성을 구현하는 매우 중요한 역할.
- 인터페이스 끼리는 다중상속이 가능하다.
    - 함수의 이름, 파라미터 타입, 파라미터 개수, 리턴타입만 약속
    - 추상클래스는 변수도 있었고, 본문이 있는 함수도 있었고, 추상함수도 있었다.
- >>추가 정보
    
    
    - 박철수 implements 의사
        - 철수는 의사의 역할을 해야되기 때문에 의사면 반드시 구현해야될 행동들을 의무적으로 구현하는 용도
        
    - interface 의사
        - 수술하다
        - 진료하다
        - 처방하다
    
    - 박철수 extends 사람
        - 철수가 가지고있는 속성과 행동의 대부분이 사람에 의해 구형되어있기 때문에 상속받는 용도
    
    - 추상클래스는 ‘존재’의 개념으로 상위개념을 뽑는 개념
    - 인터페이스는 ‘기능’의 강제화의 개념
        - 반드시 이 이름으로, 이 파라미터로, 이 리턴타입으로 함수를 재정의 해야한다는 약속

### 추상클래스 vs 인터페이스

- 공통점 : 둘 다 추상메소드를 오버라이팅 해야한다.
- 외우는것이 아니지만 진짜 이해가 안돼서 외우도록 가이드를 주자면 같은 코드를 반복해야돼서 부모의 것을 물려받아서 중복을 막는다면 추상클래스
    - 반드시 구현해야하는 기능의 약속이면 인터페이스
    - be(존재)로 구분되면 추상클래스
    - do(하는일)로 구분되면 인터페이스

### 패키지

- 패키지는 논리적 주소
- 폴더는 물리적 주소
- 실제로 서로 다른 폴더에 있더라도 패키지가 같으면 프로그램은 같은곳에 있다고 인식한다. 물리적 폴더가 없더라도 논리적으로 같은곳에 있다고 인식한다.
    - 예) a폴더 밑의 b폴더밑의 c폴더에서 import kr.co.human.클래스1
        x폴더 밑의 y폴더밑의 z폴더에서 import kr.co.human.클래스1
        같은 위치의 클래스를 가져올수 있다.
    - 예2)import kr.co.human.클래스2
        import com.google.클래스2
        클래스 이름이 같지만 오류 없이 실행된다
- 목적 : 같은 이름의 변수를 쓸 수 있게 하기 위해서.
    - 같은 이름의 변수를 서로 다른 클래스에서 쓸 수 있듯이
    - 같은 이름의클래스를 서로 다른 패키지에서 쓸 수 있다
    - 프로그램이 커지게 되면 같은 이름의 클래스가 생겨날 가능성이 높다

### 다형성 Polymorphism

- 관련개념 : 상속, 오버라이딩, 형변환
- 하나의 코드가 여러 자료형으로 구현되어 다른 실행결과를 실행하도록 하는 기술
- **하나의 객체가 여러 가지 타입을 가질 수 있는 것**
- 조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있다
- **부모는 자식을 담을 수 있지만, 자식은 부모를 담을 수 없다.**
- 남자는 사람이다. 여자는 사람이다. 는 맞는 말이지만 사람은 여자이다. 는 틀린말
- 도형 도형1 = new 원();  도형 도형2 = new 사각형();
- 자식에만 있는 멤버나 메서드는 버려진다.

- 예)
    - 함수(몬스터) 함수(플레이어) 함수(골렘)
    - 오버라이드가 작동되면서 같은 함수지만 다르게 작동.
    - 함수(캐릭터) 하나의 함수로 몬스터, 플레이어, 콜렘도 받을 수 있게 된다
    - 정보은닉, 상속과 더불어 객체지향 프로그래밍의 가장 큰 특징 중 하나
    - 다형성을 잘 활용하면 유연하고, 확장성있고 유지보수가 편리한 프로그램을 만들수 있다.

### Object클래스

- 어떤 자료형이든 상관없이 다 관리할 수 있는 자료형식.
- 모든 클래스의 최종 부모는 Object다. 그러므로 모든 클래스는 Object다.
- 객체라면 기본적으로 가지고있어야할 속성과 행동을 정의하고 있다
(모든 객체가 공통적으로 가지고있어야 할 속성과 행동이 정의되어 있다. 사실 Object 클래스에는 필드는 없다. 11개의 메소드만 있다.)
    - toString()    // 16진수로된 인스턴스의 주소를 출력
    - equals()      // 참조변수가 가르키는 값을 비교하기 때문에 주소비교. 같은 인스턴스인가
    - getClass()  // 해당객체의 클래스 타입을 반환
    

### static

- **static을 붙이면 전역변수**가 된다.

- 사용한 코드
- Main.java
    
    ```java
    package 스태틱연습;
    
    public class Main {
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    
    		Counter c1 = new Counter();
    		Counter c2 = new Counter();
    		Counter c3 = new Counter();
    		
    		
    	}
    }
    ```
    
- Counter.java
    
    ```java
    package 스태틱연습;
    
    //인스턴스가 하나 만들어 질때마다 조회수를 1 높이는 작업
    public class Counter {
    	static int count = 0;	// 정적화. 전역화 = 프로그램이 생성될때부터 꺼질때가지 유지
    		// 전역화 = 정의된 지역에 상관이 프로그램이 실행될때 생성되어 프로그램이 종료될때까지
    		// 인스턴스화 하지 않고 클래스를 컴파일할때 메모리에 올라간다
    		// 그때 올라가서 프로그램이 종료될 때까지 유지되니 '공유'라는 성질을 갖게 된다.
    	
    	public Counter() {
    		count++;
    		System.out.println("생성됨. count : "+ count);
    	}
    }
    ```
    
- 결과 : static 사용하지 않을 경우

![Untitled](/images/try_catch/Untitled%201.png)

- 결과 : static 사용한 결과

![Untitled](/images/try_catch/Untitled%202.png)

### 부동소수점

- 10진법, 2진법
- 고정 소수점 : 소수점의 위치가 고정. 정부부와 소수부로 나뉨
- 부동 소수점 : 소수점의 위치가 떠다님.  지수부와 가수부로 나뉨

- type에 대해 이해하기 위해 필요한 개념
- 코딩이랑 큰 관련 X

- 0~9 : 범위를 넘어서면 자릿수가 늘어난다.
- 인류는 손가락이 10개이기 때문에 10진법을 쓰게 되었다.
- 컴퓨터는 2진법을 쓴다.

- 컴퓨터는 2진법을 사용한다.
- 0과 1. true와 false
- 0010(2) = 0 + 0 + 1*2^1 + 0 = 2
- 1101(2) = 1*2^3 + 1*2^2 + 0 + 1*2^0 = 8 + 4 + 0 + 1 = 13

### 실습

- 반복문, 조건문, 배열을 이용하여 문제 해결
- 부족한 건 구글링으로 보충하자

- 배열에서 최댓값 찾기 + 위치 찾기
    
    ```java
    package 자바총복습;
    
    public class 배열 {
    // 9개의 서로 다른 자연수가 주어질 때, 이들 중 최댓값을 찾고
    // 그 최댓값이 몇 번째 수인지를 구하는 프로그램을 작성하시오
    // 예를 들어, 서로 다른 9개의 자연수
    // 3, 29, 38, 12, 57, 74, 40, 85, 61
    	
    // 입력 : 9개의 자연수가 들어있는 배열
    // 리턴 : 없음
    // 본문 : 최댓값과 몇번째인지 로그로 출력
    // 함수명 : printMaxValIdx
    
    // 배열, 조건문, 반복문
    	int[] arr = {3,29,38,12,57,74,40,85,61};
    	
    	public void printMaxValIdx() {
    		
    		int max = 0;
    		int count=0;
    		for(int i=0; i<9; i++) {	// 최댓값 찾기
    			if(arr[i]>max) {
    				max = arr[i];
    				count = i;
    			}
    		}
    		System.out.println("Max = " +max);
    		System.out.println("해당 숫자의 위치는 : " + count);
    	}
    }
    ```
    
- 큰 수의 각 자릿수를 배열에 담아 0~9가 몇 번 쓰였는지 출력
    
    ```java
    package 자바총복습;
    
    public class 숫자의갯수 {
    
    //세 개의 자연수 A, B, C가 주어질 때
    //AxBxC 를 계산한 결과에 각각의 숫자가 몇 번씩 쓰였는지를 구하는 함수를 작성하시오
    //예를 들어 A=150, B=266, C=427이라면
    //AxBxC=150 x 260 x 427 = 17037300이 되고,
    //계산한 결과 1703730에 0이 3번, 1이 1번, 3이 2번, 7이 2번 쓰였다
    
    //인풋 : 정수 3개
    //리턴 : void
    //본문 : 쓰여진 숫자 : 쓰여진 갯수 출력
    //
    //1. 3개의 자연수를 받은 함수 껍데기 만들기
    //2. 3개의 수를 곱한 결과값 뽑기
    //3. 0부터 9까지 반복하면서 각각의 수가 몇번 쓰였는지 파악하기
    	public void numCount(int a, int b, int c) {
    		
    		int mul = a * b * c;
    		System.out.printf("%d x %d x %d = %d \n", a, b, c, mul);
    		
    		int[] arr= new int[10];
    		int[] printNum= new int[10];
    		
    		for(int i=0; i< 10; i++) {	// 예)1000을 1 0 0 0 형태로 배열에 담기
    			arr[i] = mul % 10;		// 10으로 나눈 나머지 = 1의 자리
    			mul = mul / 10; 
    			System.out.printf("%d ", arr[i]);
    		}
    		System.out.println("");
    	
    		for(int i=0; i<10; i++) {	// 출력할 수를 printNum에 담는다
    			for(int j=0; j<10; j++) {	// printNum의 n번째 자리를 숫자 n으로 인식
    				if(arr[i]==j)		// 예)printNum의 1번째 자리가 2 = 1을 2번 사용함
    					printNum[j] += 1;
    				}
    		}
    		System.out.println();		// 결과 출력
    		for(int i=1; i<10; i++) {
    			if(printNum[i]!=0) {
    				System.out.printf("%d 이 %d 개 사용되었다. \n", i, printNum[i]);
    			}
    		}
    	}
    }
    ```
    
- 배열에 담긴 것에서 n개를 골라 더하기
    
    ```java
    package 자바총복습;
    
    public class 숫자의합 {
    //인풋 : 숫자가 담갠 배열, 자를 자릿수
    //본문 : 배열에의 첫번째요소부터 자를 자릿수만큼의 수를 모두 합친수를 출력
    //	예) 123456, 3 => 1+2+3 = 6
    //함수명 : printCuttedSum
    	
    	public void printCuttedSum(int []arr, int cut) {
    		
    		int sum=0;
    		for(int i=0; i<cut; i++) {
    			sum += arr[i];
    			System.out.printf(" %d ", arr[i]);
    			if(i!=(cut-1))
    				System.out.printf("+");
    		}
    		
    		System.out.printf("= %d", sum);
    	}
    
    }
    ```
    
- 배열에서 기준보다 작은 것 큰 것을 나눠서 출력
    
    ```java
    package 자바총복습;
    import java.util.Arrays;
    
    public class 배열나눠서오름차순출력 {
    //divideArrbyNum(int[] 인트형배열, int 기준숫자)
    //인트형 배열 안에서 기준숫자 이상인 엘리먼트 (요소=값하나)와
    //기준 숫자 이하인 엘리먼트 2개로 나눠서
    //각각 모든 요소를 오름차순으로 출력해보세요.
    //예) [1, 2, 3, 5, 7, 80, 150, 2022, 30534]
    //기준이 100이라면
    //[1,2,3,5,7,80] / [150,2022,30534] 로 나뉨
    //생각의 깊이 : 나눠서 정렬을 각각 하는거보다 처음에 정렬을 하면 한번만 하면 됨
    
    	public void divideArrbyNum(int[] arr, int criteria) {
    		
    		Arrays.sort(arr); 	// 정렬
    		
    		for(int i=0; i<arr.length; i++) {
    			if(arr[i]<criteria) {
    				System.out.printf(" %d ",arr[i]);
    			}
    		}
    		for(int i=0; i<arr.length; i++) {
    			if(arr[i]>=criteria) {
    				System.out.printf(" %d ",arr[i]);
    
    			}
    		}
    
    	}
    }
    ```