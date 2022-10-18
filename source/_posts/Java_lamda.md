---
title: "JAVA lamda"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-09-28'
---
  
### 재귀함수

- 자신을 정의할 때 자신을 리턴하는 함수
- 다시(재) 귀한(귀) 하는 함수

- [ ]  실습1
- 인자로 받은 숫자까지 1식 증가하는 모든 수를 더한 수를 리턴하는 함수를 만든다
    
    예) 함수(3) = 1 + 2 + 3 = 6
    
    // 단, 반복문 사용 금지. 재귀함수로 풀이
    

```java
public class Main {

	public static void main(String[] args) {

		System.out.println(reFunc(100));

	}
	
	static public int reFunc(int num) {
		
		if(num>1) {
			num = num + reFunc(num-1);
			return num;
		}else {
			return num;
		}
	}
}
```

### 컬렉션(Collection)

자료 : [https://st-lab.tistory.com/240](https://st-lab.tistory.com/240)

- 자바에서 미리 만들어놓은 데이터를 수집하고 관리(추가,생성,삭제,초기화,크기,리스트)해주는 목적의 클래스와 인터페이스
- 왜 사용하는가?
    - 일관된 API
    - 프로그래밍의 노력 감소
    - 프로그램 속도 및 품질 향상

- 선언법
(**중요**)   `컬렉션종류<데이터타입> 이름 = new 컬렉션종류<데이터타입>();`
예) `HashSet<String> set = new HashSet<String>();`

[**객체 리스트]**

- [ ]  Set
- 구현클래스 : HashSet, TreeSet, LinkedHashSet
- 중학교때 배웠던 "집합". 순서가 없다.  **데이터의 중복을 허용하지 않는다**.
- Hash : 임의의 길이를 갖는 데이터를 고정된 길이의 데이터로 변환(매핑)하는 것
- 해쉬는 유니크함을 보장하기 때문에 순회할 필요가 없다.
- 동일한 입력값에 대해서는 동일한 결과값(다이제스트)를 갖는다.
- 이 다이제스트의 값을 index로 활용한다.
    - 함수 : equals(), hashCode(), removeAll(), contains(값), remove(값)   add(), size()
    - 정의예 : `HashSet<String> alphabetSet = new HashSet<>();`
                `for(String spell: alphabet)`{
                    `alphabetSet.add(spell);`
                }
- HashSet의 add() = **중복된 값은 추가하지 않는다**
- Set.java
    
    ```java
    import java.util.HashSet;
    // 함수 : equals(), hashCode(), removeAll(), contains(값),
    //       remove(값)   add(), size()
    
    public class Set {
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		
    		String[] alphabet = {"a", "b", "c", "d", "e", "f", "g", "g", "a"};
    
    		HashSet<String> alphabetSet = new HashSet<>();
    		HashSet<String> alphabetSet2 = new HashSet<>();
    		
    		for(String spell: alphabet) {
    			alphabetSet.add(spell);
    			alphabetSet2.add(spell);
    		}
    		
    		alphabetSet.add("z");  // 중복없이 추가
    		alphabetSet.remove("z");
    		
    		System.out.println(alphabetSet); // 중복없이 출력
    		System.out.println(alphabetSet.contains("h"));
    		System.out.println(alphabetSet.size());
    		System.out.println(alphabetSet.equals(alphabetSet2));
    		
    	}
    
    }
       
    ```
    

- [ ]  List
- 구현클래스 :  ArrayList, LinkedList, Vector
- 순서가 있는 데이터의 집합으로 **데이터의 중복을 허용**
    - 함수 : add(값),  addAll(리스트),   remove(인덱스),   clear(),   size()
              get(인덱스),   indexOf(값),   lastIndexOf(값)
- 반복문과 결합 :   `향상된for문  for(자료형 이름 : 리스트)`
                     `while(iterator.hasNext())`
- 예제)

```java

    // ArrayList 선언
    ArrayList<Integer> al = new ArrayList<Integer>();

    // ArrayList에 데이터 입력
    for (int i = 1; i <= 5; i++)
        al.add(i);

    // 결과 출력
    System.out.println(al);   //[1, 2, 3, 4, 5]

    // **인덱스 제거**하기
    al.remove(3);

		// **값으로 제거**하기
		al.remove(al.indexOf(5));
		al.remove(Integer.valueOf(3)); // 값 지우기 : 오버로딩 사용
		System.out.println(al);

    // 결과 출력
    System.out.println(al); //[1, 2, 3, 5]

    // 하나씩 가져와서 결과 출력
    for (int i = 0; i < al.size(); i++)
        System.out.print(al.get(i) + " ");  //1 2 3 5

```

- [ ]  Queue
- 구현클래스 :  LinkedList, PriorityQueue
- [ ]  Map
- 구현클래스 : Hashtable, HashMap, TreeMap
- 키(Key), 값(Value)의 쌍으로 이루어진 데이터의 집합
- 함수 리스트
add(), remove(), clear(), size()
    - // 직접 위의 함수들 구현해보는 것도 좋은 공부다
    - private int[] nums,    private int current;

### String 문자열 클래스

- 이제야 눈에 보이는 스트링. 원시타입이 아니다
- 자바에서 컬렉션으로 만들어 놓은 자료구조다
- charAt(), compareTo(), concat(), indexOf(), trim(), toLowerCase(), toUpperCase(), substring, length(), isEmpty(), contains() 문자의 위치반환 없으면-1, matches(정규식) 등의 함수가 있다
- 스트링은 값이 달라질 때 새로운 객체를 만들어서 할당받는다

```markdown

//자바에서 문자열1에서 문자열2를 포함한 갯수 찾기
```java
	  public int getCountInclude(String str1, String str2){
	      boolean include = true;
	      int count = 0;
	      include = str1.contains(str2);	//포함되었는지 참,거짓 판단
	      while(include) {	//포함되었다면
	         count++;
	         int where = str1.indexOf(str2);	//시작하는 위치 파악
	         str1 = str1.substring(where+str2.length());
	         System.out.println("str1 : "+str1);
	         //방금 찾은 거를 빼고 남은 문자열을 부모로 업데이트
	         //substring 함수는 인자가 하나면 해당 위치부터 이후로 끝까지 자르는 함수
	         include = str1.contains(str2);
	      }
	      return count;
	   }

```
```

### 제네릭(Generic)

- 뜻 :  포괄적인, 일반적인
- Object 를 만들면 사용(저장, 로드)하기전에 형변환 작업을 해줘야 하는 불편함이 존재한다.
- 범용 컬렉션의 장점과 특화된 클래스의 장점을 모두 겸비한 템플릿.
- Java5에서 추가
- 컬렉션, 람다식, 스트림, NIO(New IO)등에서 널리 사용되므로 제네릭을 이해하지 못하면 API 문서를 정확히 이해할 수 없다.

- 목적
- 자료형을 일반화. 정의시가 아니라 인스턴스 생성시 자료형을 결정하도록 한다.
- 우리가 어떤 자료구조를 만들어서 배포하려고 할때 '여러 데이터타입을 지원하고 싶다.'  그러면 String에 대한 클래스, Integer에 대한 클래스 등등을 하나하나 타입별로 만들어줘야하나? 너무 비효율적이다.

- 제네릭은 이런 문제를 해결해준다.
- 그렇게 강조했던 메소드의 정의와 호출 다시한번 보자. 어떤 이름으로 넘어오든지 정의한 영역내에서는 이 이름으로 쓰겠다는 뜻이었던가?
- 마찬가지로 제너릭이라는 것은 어떤 데이터타입으로 넘어오든지 이 정의한 영역내에는 넘어온 그 데이터타입으로 쓰겠다 라고 하는것이다.
- 즉 데이터형을 정의시 명시하지 않고 호출할때 정할 수 있도록 일반화 한것이다.
- 클래스 내부에서 지정하지 않고 외부에서 지정도록 한 것이다.
- 엄밀히 말하자면 컴파일때 해당 타입으로 캐스팅하는 것이다.

- 사용 예시
    
    ```java
    import java.util.List;
    import java.util.ArrayList;
    
    public class 제네릭 {
    	// 함수의 정의와 호출이 다르다. 파라미터와 아큐먼트는 다르다
    	
    
    	public static void main(String[] args) {
    		
    		//일반
    		List list = new ArrayList();
    		list.add("hello");
    		String str = (String)list.get(0);
    		System.out.println(str);
    		
    		//제네릭사용한 코드 < 데이터 타입>
    		List<String> list2 = new ArrayList<String>();
    		list2.add("hello");
    		String str2 = list2.get(0);
    		System.out.println(str2);
    		
    	}
    
    	
    }
    ```
    

```markdown
public class Box<T>{
    // 클래스 뒤에 <T> 타입 파라미터를 명시했기 때문에 변수의 타입으로 사용 가능합니다.
    private T t;
    public T get() { return t; }
    public void set(T t){ this.t = t; }
}

```

- 특징
- 보편적(암묵적)으로 매개변수의 타입으로는 아래의 이름을 쓴다.
    <E> : Element
    <K> : Key
    <N> : Number
    <T> : Type
    <V> : Value
- 특정범위 내로 좁혀서 제한하고 싶다면 extends, super, ? 를 활용한다.
- 예를들어 <K super T>이면 T타입의 조상만 가능하고 K로 쓰겠다는 말이다.

- 문법
- 정의 : 클래스 또는 인터페이스 이름 뒤에 <타입파라미터>
- 생략하면 컴파일러가 제네릭 관련 문장에서 자료형의 이름을 추론한다. 이걸 다이아몬드 표시라고 한다.
- 타입 파라미터로 명시할수 있는 것은 참조타입만 가능하다.
- 여러 개의 타입변수는 쉼표로 구분하여 명시한다.
- 사용 : 본문에서 그 이름을 데이터타입처럼 사용하면 된다.

- 장점
1. 런타임에 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지함
2. 반환값에 대한 타입 변환(캐스팅) 및 타입검사에 들어가는 노력 줄어듬
3. 코드의 재사용성이 높아

### 람다식(Lamda Expression)

- 자바8에 함수적 프로그래밍 기법으로 도입됨. 람다가 포함되면서 자바가 완전해졌다고 말하는 이가 있을 정도
- 익명함수를 생성하기 위한 식
- y = f(x) 형태를 (타입 매개변수) -> { 실행문 } 으로 정의
좋든 싫든 자바의 람다식은 선택이 아닌 필수가 되었다
- 장점 : 1. 코드가 매우 간결해진다
          2. 인스턴스 생성안하고 기능하나만 필요할 때
          3. 컬렉션요소를 매핑해서 쉽게 집계할 수 있다
- 단점 : 1. 가독성이 안좋아진다.
 2.함수이름이 없기 때문에 stacktrace보고 디버깅하기 어렵다.
  3. 이 함수가 있음을 인식하기가 어렵다
- 결론 : 저런 단점들 때문에 고급개발자는 람다식 쓰지말라고도 하는 사람 많다.
- 코드가 3줄안에 끝나고 단 한번만 쓰임을 보장할 수 있고 행동이 명확할 때만 제한적으로 사용
- 문법 : 인풋데이터 -> 함수본문
    - 예  :1. 줄임이 없는 예
      `(String s) -> { System.out.println(s); }`
    
      2. 매개변수가 하나일 때 괄호생략. 본문이 하나일 때 중괄호와 세미콜론 생략
       `s -> System.out.println(s)`
       `(a,b) -> a+b`
    
      3. 제네릭으로 사용한 예
      `Calculate<Integer> ci = (a,b) -> a+b;`
      `System.out.println(ci.cal(4,3));`