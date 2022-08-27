---
title: "JAVA OOP practice"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-08-20'
---
  
- 상속, 클래스 등을 이용해 RPG 만들어보기 

### 복습

- 오버라이딩
    
    = 오버라이트로 기억
    
    = 덮어쓰기. 부모의 자식을 새롭게 함수 정의
    
- 오버로딩
    
    = 파라미터 타입이나 갯수가 다를 때 이름이 같으면서 새롭게 함수 정의
    
    // 새 이름을 고민하는 시간 단축
    
    // 이름은 그 함수가 하는 일이 함축되어 있기 때문에 하는 일이 같음을 유추 가능
    
- 객체
    
    = 우리가 프로그램으로 구현할 대상
    
    = 자바에서는 class로 객체를 설계한다
    
    = 생성자를 통해 인스턴스를 만든다
    
    = 인스턴스가 되어야 비로소 메모리에 올라가고 실체화 된다
    
    = 객체는 변수와 메소드의 묶음이다. 속성과 행동의 묶음이다.
    

- 생성자
    
    = 인스턴스를 만들 때 new 키워드와 함께 쓰인다
    
    = 함수와 비슷하게 생겼지만 이름이 클래스와 같고, 리턴타입이 없다
    
    = 인스턴스를 만들 때 반드시 필요한 데이터를 강제하는 역할을 한다
    
    // 준비되지 않은 상태라면 인스턴스를 만들 수 없도록 한다.
    
    - 추가 정보
        - 생성자를 명시하지 않은 경우 컴파일러가 자동으로 부모의 디폴트 생성자를 호출한다. super();
        - 그렇기 때문에 부모의 사용자정의생성자가 있는데도, 자식에서 부모의 생성자를 호출하지 않는다면 컴파일 에러가 발생한다.
        - 자기의 생성자안에는 최종 조상이 있어야 되는 이런 매커니즘은 최종 조상인 object를 생성할 대까지 계속 된다.
            
            자식 > 부모 > 조부모 > 조무보의 부모 …… > Object
            
        - 사용자 정의 생성자가 하나라도 있으면 디폴트 생성자는 호출되지 않는다
        
        // super()를 를 호출했는데 그 생성자는 없기 때문
        

- 추상클래스
    
    = abstract 키워드가 붙은 메소드 (추상메소드)가 하나라도 포함된 클래스를 말한다
    
    = 클래스 앞에도 abstract 키워드를 붙여줘야 한다
    
    = 목적 : 상속
    
    : 미구현된 함수가 있으니 반드시 자식에서 오버라이딩 해야함을 명시적으로 알려준다
    
    : 미구현된 함수 마고는 자식에서 그대로 상속받아 사용할 수 있다.
    

- 상속
    
    = 자식 클래스 extends 부모 클래스
    
    = 를 하면 부모의 변수와 메소드를 자식에서 코딩하지 않고도 그대로 사용할 수 있다
    
    = 부모클래스는 하나밖에 못둔다
    
    = 동시에 2개 이상의 클래스로부터 상속받을 수 없다.
    
    - 추가 정보
        
        = 내가 부모클래스를 만들어 상속을 만들려고 함다면 is a 관계인지 확인해야한다
        
        = has a 관계로 상속관계를 구현하는 실수를 하기 쉽다
        
        = 사각형은 도형’이다’ O
        
        = 도형은 사각형’이다’ X 
        
        - 부모에 선언된 변수와 같은 이름으로 자식에 선언하면 자식의 것이 사용된다. (오버라이딩 개념)
        
          ⇒ 나로부터 타고 올라간다.
        
        - 부모에 변수가 있어도 자식에 있으면 자식 것으로 덮어쓰기 때문
            
            → 최대한 부모에 있는 변수와 같은 이름으로 자식에 쓰지말고
            
            → 쓸 경우가 생겼다면 부모에만 넣고 지식에 없애면
            
        
         -예를 들어, name이라는 값을 썻으면 먼저 나한테 그 변수가 있나 찾는다
        
         - 없으면 나의 부모를 찾는다
        
         - 부모에게 없다면 부모의 부모를 찾는다
        
         - 이런 방식으로 최종 부모인 Object까지 훑고 올라간다
        
         - 정리하자면 나부터 타고올라가기 때문에 동시에 잇다면 내것이 우선된다
        
         - 나한테 없더라도 내 조상 누군가에 있다면 그것을 쓸수 있다.
        
         → 부모에 있는 나한테 또 정의해놨을 경우
        
         - 부모에서 변수를 사용하면 부모의 것이 사용되지 자식의 것이 사용되지 않는다
        
         - 자식에서 변수를 사용하면 자식의 것이 사용되지 부모의 것이 사용되지 않는다. 
        

- 접근제한자
    
    = 역할 : 접근을 제한하는 역할.
    
    = 왜 접근을 제한하나요? 다른 사람 (다른 클래스)가 함부로 나의 값에 접근하거나 수정하는 것을 막기 위해서
    
    = 노출시키지 않고 싶거나, 노출시키면 안되는 정보들이 있기 때문에
    
    - private : 자기 클래스에서만 사용
    - default : 해당 패키지 내에서만
    - protected : 해당 패키지 + 상속받은 클래스
    - public : 이 프로젝트내 어디서나

---

 

### 학습목표

1. rpg 완성
    - Player 클래스와 Monster 클래스에 중복된 코드를 Character를 상속받는 코드로 업그레이드
    - 객체는 call by reference이기에 객체를 출력하면 객체의 값이 아니라 주소가 출력된다
    - 객체를 출력했을 때 자동으로 호출되는 함수가 toString이고 사용자정의하지 않았다면 기본적으로 주소가 출력된다.
    - toString을 통해 값을 출력하도록 만들 수 있다
    - 이클립스에서 우클릭 source - generate toString 들어가서 변수들 체크해주면 값들 찍히게 됨
    
    f3 : 정의부로 이동
    
    상속 추가 설명
    
    구현실습
    
    캐릭터에 상속바디 완료.zip
    
    접근제한다
    
    getter, setter
    
2. 이클립스 단축기 복습
- ctrl + space : 자동완성
- ctrl + shift + r : 파일명으로 바로 찾기
- ctrl + d : 한줄 지우기
- ctrl + alt +키보드아래 : 해당블록 복붙
- f3 : 정의부로 이동
- alt + shift + s : Source
- ctrl + shift + 0 : 자동 import
- ctrl +shift + f : 자동 들여쓰기
- ctrl + shift + p : 짝 괄호로 이동

1. 메소드 복습
- 파라미터
    - parameter = 매개변수 = 정의할 때 사용한 변수

- 아큐먼트
    - argument = 전달인자 = 호출할 때 사용한 값

```java
String a = 'a';
public a(String a){
		return a;
}
a(a);
```

오버로딩, 오버라이딩

1. 로또 번호 추출
    
    랜덤
    
    배열
    
    Game, Lotto
    

### 팁

- F3
    - 호출한 함수에 F3을 찍으면 정의된 함수 위치로 이동한다

---

 

### 실습 - RPG

- [Game.java](http://Game.java) 가 main 파일이다
- Game.java
    
    ```java
    public class Game {
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		
    		Player player1 = new Player("kmk");
    		Monster enemy1 = new slime("빨간슬라임", 100);
    		enemy1.attack(player1);
    		
    //		player1.attack(enemy1);
    //		player1.attack(enemy1);
    //		player1.attack(enemy1);
    //		player1.attack(enemy1);
    //		player1.attack(enemy1);
    //		player1.attack(enemy1);
    		// 죽으면 죽었다고 알려주기
    		// 죽은 몹에게 공격못하기
    		
    		// 무기를 하나 만들어서 그 무기를 장착하면
    		// 해당 무기의 데미지만큼 플레이어의 데미지를 올려주세요
    		Weapon weapon1 = new Weapon();
    		weapon1.name = "창";
    		weapon1.damage = 20;
    		Weapon weapon2 = new Weapon();		
    		weapon2.name = "활";
    		weapon2.damage = 35;
    		
    		player1.setWeapon(weapon2);
    		player1.attack(enemy1);
    		
    		Potion healPotion = new Potion("회복포션(소)", 30, "빨간색", "회복");
    		System.out.println(healPotion.name);
    		
    		Potion manaPotion = new Potion("마나포션(소)", 30, "파란색", "마나회복");
    		System.out.println(manaPotion.name);
    		
    		Golem gol1 = new Golem("바위골렘", 1000);
    		System.out.println(gol1.hp);
    		gol1.defenceOn();
    		player1.attack(gol1);
    		
    		
    		
    		
    	}
    
    }
    ```
    
- Monster.java
    
    ```java
    // 내부에 미구현인 abstract 클래스가 하나라도 있으면 abstract라 표시
    public abstract class Monster {
    	String name;
    	int hp = 100;
    	int mana = 50;
    	int damage = 10;
    	String kind;
    	
    	public Monster(String name, int hp) {
    		this.name = name;
    		this.hp = hp;
    	}
    	
    	public void attack(Player player) {
    		if(player.hp<=0) {
    			System.out.println(player.name+"은(는) 이미 죽은상태라 공격할수 없습니다");
    			return;
    		}
    		int afterhp = player.hp - this.damage;
    		System.out.printf("%s이(가) %s를 %d의 데미지로 공격합니다.\n", this.name, player.name, this.damage);
    
    		if(afterhp<0) {	//적이 이번공격에 죽은경우
    			afterhp = 0;
    			System.out.printf("적이 이번공격에 죽었습니다.\n");
    			player.hp = afterhp;
    			return;
    		}
    		System.out.printf("%s의 체력이 %d에서 %d가 되었습니다.\n", player.name, player.hp, afterhp);
    		player.hp = afterhp;
    	}
    	
    	public void powerUp() { 
    		this.damage *=2;
    	}
    	
    }
    ```
    
- Player.java
    
    ```java
    public class Player {
    	//name, hp, mana, damage
    	//attack, skill1, skill2
    	String name;
    	int hp = 100;
    	int mana = 100;
    	int damage = 20;
    	
    	
    	
    	public Player(String name) {
    		//this 가 자기자신이고 super는 부모다.
    		//super();	//부모의 기본생성자를 호출한거다.
    		this.name = name;
    	}
    
    	public void attack(Monster enemy) {
    		
    		if("골렘".equals(enemy.kind)) {
    			if(this.damage <= 40) {
    				this.damage = 0;
    			}else {
    				this.damage -= 10;
    			}
    			System.out.println("골렘은 10의 데미지를 차감합니다.");
    		}
    		
    		
    		if(enemy.hp<=0) {
    			System.out.println(enemy.name+"은(는) 이미 죽은상태라 공격할수 없습니다");
    			return;
    		}
    		int afterhp = enemy.hp - this.damage;
    		System.out.printf("%s이(가) %s를 %d의 데미지로 공격합니다.\n", this.name, enemy.name, this.damage);
    
    		if(afterhp<0) {	//적이 이번공격에 죽은경우
    			afterhp = 0;
    			System.out.printf("적이 이번공격에 죽었습니다.\n");
    			enemy.hp = afterhp;
    			return;
    		}
    		System.out.printf("%s의 체력이 %d에서 %d가 되었습니다.\n", enemy.name, enemy.hp, afterhp);
    		enemy.hp = afterhp;
    	}
    	
    	public void setWeapon(Weapon weapon) {
    		System.out.printf("%s 장착완료. 데미지 %d증가. \n", weapon.name, weapon.damage);
    		this.damage += weapon.damage;
    	}
    }
    ```
    
- Character.java
    
    ```java
    public class Character {
    	String name;
    	int hp;
    	int mana;
    	int damage;
    	String kind;
    	
    	public Character() {
    	
    		
    	}
    	
    	public void attack(Character obj) {
    		if(obj.hp<=0) {
    			System.out.println(obj.name+"은(는) 이미 죽은상태라 공격할수 없습니다");
    			return;
    		}
    		int afterhp = obj.hp - this.damage;
    		System.out.printf("%s이(가) %s를 %d의 데미지로 공격합니다.\n", this.name, obj.name, this.damage);
    
    		if(afterhp<0) {	//적이 이번공격에 죽은경우
    			afterhp = 0;
    			System.out.printf("적이 이번공격에 죽었습니다.\n");
    			obj.hp = afterhp;
    			return;
    		}
    		System.out.printf("%s의 체력이 %d에서 %d가 되었습니다.\n", obj.name, obj.hp, afterhp);
    		obj.hp = afterhp;
    	}
    	
    }
    ```
    
- slime.java
    
    ```java
    
    ```
    

### 실습 - Lotto

- Game.java가 main 파일이다
- Game.java
    
    ```java
    package 로또;
    
    public class Game {
    
    	public static void main(String[] args) {
    //		System.out.println((int)(Math.random()*100));
    		Lotto lotto = new Lotto();
    		lotto.makeLotto();
    		System.out.println(lotto);
    
    		Player p1 = new Player("배성원");
    		p1.buyLotto(5);
    	}
    }
    ```
    
- Lotto.java
    
    ```java
    package 로또;
    import java.util.Arrays;
    import java.util.Random;
    
    public class Lotto {
    	//1~45범위에서 중복없이 6개의 번호가 있다
    	int [] numArr = new int [6];
    	
    	//1. 1부터 45까지의 랜덤 번호 생성
    	//2. 배열에 넣기
    	//3. 중복이 있으면 다시 뽑기
    	//4. 오름차순으로 정렬
    
    	public int getRandomNum(int startNum, int endNum) {
    		Random rd = new Random();
    		int numArr;
    		numArr = rd.nextInt(endNum)+ startNum; // 0~endNum + startNum
    		// nextInt(int a) = 0부터 a미만의 랜덤 정수를 리턴
    		// 거기에 startNum를 더하면 starNum부터 a+startNum미만의 랜덤정수를 리턴
    		// 0부터 45 미만의 수를 뽑아서 1을 더하니까 1부터 46미만의 수를 얻게되는 것
    //		System.out.println(num);
    		return numArr;
    	}
    	public Lotto makeLotto() {
    		// 1.리턴이 void에서 Lotto로 변경
    		// 2.실체화된 인스턴스를 리턴해야 됨
    		// 3.int 6개짜리 변수에 랜덤값을 담아 그 Lotto 인스턴스를 반환
    		// 4.this로 바꾸는 게 더 좋다
    
    		Lotto lotto = new Lotto();
    		int [] newNumberList = new int[6];
    		for(int i=0; i<6; i++) {
    			int randomNum = getRandomNum(1, 45);
    			// 넣기 전에 중복된 것이 있나 검사
    
    			boolean isdup = findDup(numArr, randomNum);
    			if(isdup == true) {						// 중복이 있다면
    //				System.out.printf("%d%s \n", i+1, "번째 숫자 뽑을 때 중복 발생."); 
    				randomNum = getRandomNum(1, 45);    // 새로 뽑기
    //				System.out.println("새로 뽑은 값: " + randomNum);
    				i--;	// 다시 뽑은 것이 중복일 대를 대비하여 방금뽑은걸 다시 검사
    			}else { 
    				newNumberList[i]=randomNum; // 새로뽑은 숫자 현재 자리에 넣기
    			}
    		}
    		sort(newNumberList);
    		lotto.numArr = newNumberList;
    		return lotto;
    	}
    	
    	public boolean findDup(int[] arr, int targetNum) {
    		//기존의 배열의 값에서 중복된 것이 있나 검색
    		for(int i=0; i<arr.length; i++) {
    			if(arr[i] == targetNum) {
    				return true;
    			}
    		}
    //		System.out.println("중복안됨");
    		return false;
    	}
    	
    	public void sort(int[] arr) {
    		Arrays.sort(arr);
    		// 정렬 함수
    	}
    	@Override
    	public String toString() {
    		return "Lotto [num=" + Arrays.toString(numArr) + "]";
    	
    }
    ```
    
- Player.java
    
    ```java
    package 로또;
    import java.util.Arrays;
    
    public class Player {
    	
    	String name;
    	Lotto[] lottoList;
    			
    	public Player(String name) {
    		super();
    		this.name = name;
    		// TODO Auto-generated constructor stub
    	}
    	public void buyLotto(int n) {
    		lottoList = new Lotto[n];	// 인자로 받은 크기로 지정
    		for(int i=0; i<n; i++) {
    			Lotto lotto = new Lotto();
    			lottoList[i] = lotto.makeLotto();
    			System.out.println("로또 구매 : "+lottoList[i]);
    		}
    		// 로또 n 개를 뽑기
    		// 뽑은 로또를 내가 보유하고 있는 로또 리스트에 넣기	
    	}
    	@Override
    	public String toString() {
    		return "Player [name=" + name + ", lottoList=" + Arrays.toString(lottoList) + "]";
    	}
    }
    ```
    

### 배열 (array)

- 동일한 자료형'의 '순차적'인 자료구조
- 같은 데이터타입의 연관된 여러개의 데이터를 하나의 변수에 담아서 쉽게 관리할수 있도록 해주는 자료구조중 하나
- 인덱스는 0부터 시작한다.
- 장점 : 인덱스를 활용하여 빠른 참조가능
- 단점 : 크기가 선언시의 크기에서 바꿀수 없다.

- 생성법 : 자료형[] 배열이름 = {값1, 값2, 값3...};

`자료형[] 배열이름 = new 자료형[크기];`

- 사용법 : 배열이름[인덱스];

배열의 모든요소 출력 : 반복문쓰거나 Arrays.toString(배열명)

- 크기 할당 & 초기화 없이 배열 참조변수만 선언

`int[] arr;`

`int arr[];`

- 선언과 동시에 배열 크기 할당

`int[] arr = new int[5];`

`String[] arr = new String[5];`

- 기존 배열의 참조 변수에 초기화 할당하기

`int[] arr; arr = new int[5];` 

//5의 크기를 가지고 초기값 0으로 채워진 배열 생성

- 선언과 동시에 배열의 크기 지정 및 값 초기화

`int[] arr = {1,2,3,4,5};`

`int[] arr = new int[] {1,3,5,2,4};`

`int[] odds = {1,3,5,7,9};`

`String[] weeks = {"월","화","수","목","금","토","일"};`

// 2차원 배열 선언

`int[][] arr = new int[4][3];` //3의 크기의 배열을 4개 가질 수 있는 2차원 배열 할당

`int[][] arr9 = { {2, 5, 3}, {4, 4, 1}, {1, 7, 3}, {3, 4, 5}};`

```

### **주소값 비교(==)와 값 비교(equals)**

- 원시형 8가지 type이 아니라면 (==) 는 주소값을 비교한다
- 이런 경우에 실제 값을 비교하려면 equals를 사용

> ==연산자와 equals()메소드의 가장 큰 차이점은 == 연산자는 비교하고자 하는 두개의 대상의 주소값을 비교하는데 반해 String클래스의 equals 메소드는 비교하고자 하는 두개의 대상의 값 자체를 비교한다는 것입니다. 기본 타입의 int형, char형등은 Call by Value 형태로 기본적으로 대상에 주소값을 가지지 않는 형태로 사용됩니다. 하지만 String은 일반적인 타입이 아니라 클래스입니다. 클래스는 기본적으로 Call by Reference형태로 생성 시 주소값이 부여됩니다. 그렇기에 String타입을 선언했을때는 같은 값을 부여하더라도 서로간의 주소값이 다릅니다.
> 

### 실습 - 배열

- 배열 선언법 정리
- ==와 equal 차이 비교
- 랜덤숫자 맞추기 게임 구현으로 응용

- 배열 연습
    
    ```java
    package 배열;
    
    import java.util.Arrays;
    import java.util.Random;
    import java.util.Scanner;
    
    public class Main {
    	
    	public static void main(String[] args) {
    		
    		// 초기화 = 정의 후에 값 할당까지 한 번에 하는 것
    		int intArr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    		
    		int[] intArr3;
    		intArr3 = new int[]{1,2,3,4,5,6,7,8,9,10}; // Java 형식
    		
    //		if(intArr == intArr3) {
    //			System.out.println("같음");
    //		}
    		
    		String[] strArr1 = {"일", "이", "삼"};
    		// 스트링배열을 스트링으로 변환할 수 없습니다.
    		
    		int twoMension[][] = {{1, 2, 3}, {5, 10, 15}};
    //		System.out.println(twoMension.length);
    //		System.out.println(twoMension[1]);
    		
    		
    		// 향상된 for문. iterator = 반복할수 있는 객체
    		// iterator의 모든요소에 대해서 반복을 수행
    //		for(int i : twoMension[1]) {
    //			System.out.print(i + " ");
    //		}
    //		System.out.println("");
    		
    		int [][][] threeDemension = new int[2][4][6];
    		// 뒤에서부터 읽는다.
    		// 2개짜리가 4개 있고 그런 놈이 6개있다. X
    		// 6개짜리가 4개 있고 그런 놈이 2개있다. O
    		
    //		System.out.println(threeDemension.length);
    		
    		String[] 계절 = {"봄", "여름", "가을", "겨울"};
    		String[] 복사본 = 계절;		// 배열의 복사. 그냥 =으로 하면 얕은 복사.
    		String[] 진짜복사본;
    //		String[] 진짜복사본2 = new String[];
    		
    		
    		boolean result = Arrays.asList(계절).contains("핵겨율");
    //		System.out.println(result);
    //		if( 계절 == 복사본) {
    //			System.out.println("복사본 : 같다");
    //		}else {
    //			System.out.println("복사본 : 틀리다");
    //		}
    		 
    		진짜복사본 = 계절.clone();
    //		if( 계절 == 진짜복사본 ) {
    //			System.out.println("진짜복사본 : 같다");
    //		}else {
    //			System.out.println("진짜복사본 : 틀리다");
    //		}
    		
    		// 깊은 복사를 하기 위해서 반복문을 돌리든가, system.arraycopy() 메소드를 이용
    //		System.arraycopy(계절, 0, 진짜복사본2, 0, 계절.length);
    //		if(계절 == 진짜복사본2) {
    //			System.out.println("진짜복사본2 : 같다");
    //		}else {
    //			System.out.println("진짜복사본2 : 틀리다");
    //		}
    		
    		// 영단어가 저장된 배열. 크기는 5. endDic
    			// apple, banana, peach
    		// 한글단어가 저장된 배열. 크기는 5. korDic
    			// 사과, 바나나, 복숭아
    		// 한글랜덤단어를 보여주고
    		// 유저는 영단어를 치고
    		// 답이 맞는지 틀렸는지 판단
    //		System.out.println("키보드로 뭔가를 입력해보세요 : ");
    //		Scanner sc = new Scanner(System.in);	// 캐보드로 입력받기 위한 객체 생성
    //		String input = sc.next();
    //		System.out.println(input);
    
    	}
    }
    ```
    
- 영단어 맞추기
    
    ```java
    package 배열;
    
    import java.util.Arrays;
    import java.util.Random;
    import java.util.Scanner;
    
    public class Main {
    	
    	public static void main(String[] args) {
    		
    		
    		// 영단어가 저장된 배열. 크기는 5. en1
    			// apple, banana, peach
    		// 한글단어가 저장된 배열. 크기는 5. kor1
    			// 사과, 바나나, 복숭아
    		// 한글랜덤단어를 보여주고
    		// 유저는 영단어를 치고
    		// 답이 맞는지 틀렸는지 판단
    //		System.out.println("키보드로 뭔가를 입력해보세요 : ");
    //		Scanner sc = new Scanner(System.in);	// 캐보드로 입력받기 위한 객체 생성
    //		String input = sc.next();
    //		System.out.println(input);
    		
    		String en1[];
    		en1 = new String[]{"apple", "banana", "peach", "watermelon", "pineapple"};
    		String kor1[];
    		kor1 = new String[]{"사과", "바나나", "복숭아", "수박", "파인애플"};
    		
    		Random rd = new Random();
    		int randomInt = rd.nextInt(5);
    //		System.out.println(randomInt);
    		
    //		System.out.printf("%d. %s을(를) 영어로 입력해주세요 : ", randomInt, kor1[randomInt]);
    		
    		Scanner sc = new Scanner(System.in);	// 캐보드로 입력받기 위한 객체 생성
    //		String input = sc.next();
    //		System.out.println(input);
    		
    //		if(input == en1[randomInt]) {
    //			System.out.println("정답입니다!!!");
    //		}else {
    //			System.out.println("오답입니다");
    //		}
    //		
    //		if(input.equals(en1[randomInt])) {
    //			System.out.println("정답입니다!!!");
    //		}else {
    //			System.out.println("오답입니다");
    //		}
    
    		
    		//  문자열 1 == 문자열 2 값을 비교하는게 아니라 주소값 비교
    		// 문자열1.equals(문자열2) 값을 비교. 순서 상관 없음.
    	}
    }
    ```
    
- 랜덤 숫자 맞추기 놀이
    
    ```java
    package 배열;
    
    import java.util.Arrays;
    import java.util.Random;
    import java.util.Scanner;
    
    public class Main {
    	
    	public static void main(String[] args) {
    		
    		// 컴퓨터가 랜덤 1~100 까지의 랜덤 숫자 하나를저장
    		// 유저가 5번의 기회동안 그 숫자를 찾는 게임
    		// 답이 제출한수 보다 높은지, 낮은지 알려준다
    		// 게임이 끝나면 이때까지 유저가 제출했던 답과 컴퓨터의 답을 보여주세요
    		
    		int randomInt2 = rd.nextInt(100)+1;
    		
    		int[] myAnswer = new int[5];
    		
    		int count=1;
    		int i=0;
    		while(count==1) {
    			
    			System.out.printf("1~100 사이의 숫자를 입력해주세요 : ");
    			int inputNum = sc.nextInt(); 
    //			System.out.println(inputNum);
    			
    			
    			if(randomInt2 == inputNum) {
    				System.out.println("정답입니다");
    				count --;
    			}else {
    				System.out.printf("다시 입력해주세요 %d %d \n", randomInt2, inputNum);
    				
    				if(randomInt2 > inputNum) {
    					System.out.println("더 높은 숫자입니다");
    				}else {
    					System.out.println("더 낮은 숫자입니다");
    				}
    				myAnswer[i] = inputNum;
    				System.out.printf("==================== \n");
    			}
    			i++;
    			
    			if(i==5) {
    				count--;
    			}
    		}
    		System.out.printf("==================== \n");
    		System.out.printf("==================== \n");
    		System.out.printf("==================== \n");
    		System.out.printf("지금까지 입력했던 답입니다 :");
    		for(int j=0; j<myAnswer.length; j++) {
    
    			if(myAnswer[j]==0) {
    				continue;
    			}
    			else {
    				System.out.printf("% d ", myAnswer[j]);
    			}	
    		}
    		System.out.println("");
    		System.out.printf("정답을 공개합니다 : %d", randomInt2);
    		
    	}
    }
    ```