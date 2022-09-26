---
title: "JAVA thread"
tags:
  - Java
categories:
  - Java
  - 기초문법
author: "minkuen"
date: '2022-09-18'
---

# Java_0620

### 상수와 enum

- [ ]  **final 키워드**
- final에 초기값을 줄 수 있는 경우는 2가지 뿐이다
- 필드선언 시, 생성자
- 초기화되지 않은 final 필드가 남아있으면 컴파일 에러
- 진짜 상수는 static final로 선언. 객체마다 저장할 필요가 없으며 다른값으로 바꿀수도 없기 때문이다
- 명명규칙 : 대문자에 언더바 조합 

 

- [ ]  **enum은 열거형(Enumeration)**. **상수의 그룹을 나타낸다.**
- 주목적 : 우리만의 데이터 타입을 가지기 위해서
- 모든 enum들은 내부적으로 java.lang.Enum 클래스에 의해 상속된다.
- 만드는 문법 : `enum 열거체이름 { 상수1이름, 상수2이름, ... }`
    - 예) `enum Rainbow { RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET }`
- 사용문법 : 열거체이름.상수이름
    - `Rainbow.RED`
    
- [ ]  메소드
- **values**() 모든 상수 배열로 반환
    - 예) `Rainbow[] arr = Rainbow.**values**();`
- **ordinal()**	상수 인덱스 반환.
    - 예) `int idx = Rainbow.YELLOW.**ordinal**();`
- **valueOf()**	 상수 문자 값 반환
    - 예) `Rainbow rb = Rainbow.**valueOf**("GREEN");`
    

### 실습-enum

- Main.java
    
    ```java
    public class Main {
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		
    		String 요일 = "TUESDAY";
    		Test t1 = new Test(Day.valueOf(요일));
    		t1.요일평가();	
    	}
    }
    ```
    
- Test.java
    
    ```java
    public class Test {
    
    	Day day;
    	
    	public Test(Day day) {
    		this.day = day;
    	}
    	
    	public void 요일평가() {
    		switch(day) {
    		case MONDAY:
    			System.out.println("월요일은 좋지 않음");
    			break;
    		case FRIDAY:
    			System.out.println("금요일은 좋음");
    			break;
    		case SATURDAY:
    		case SUNDAY:
    			System.out.println("주말은 최고지");
    			break;
    		default:
    			System.out.println("평법합니다.");
    			break;
    		}
    	}
    }
    ```
    
- Day.java
    
    ```java
    	// 문법 : enum 이름{값 값 값}
    public enum Day {
    	
    	SUNDAY, MONDAY, TUESDAY, WHEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    	
    }
    ```
    

---

### 사전지식

- 프로그램 : 어떤 작업을 위해 실행할 수 있는 파일
- 프로세스 : 실행되고 있는 프로그램.   실행되기 위해서는 메모리에 올라와야 한다. 프로세스는 운영체제로부터 자원을 할당받는다. 1개의 프로세스는 최소 1개의 스레드를 가지고있다.
    - 예) 크롬을 켜서 유튜브를 보고있는동시에 마우스를 움직이는 동시에 파일은 다운 받아지고 있다.
    - 예) 햄버거를 시키면 그릴에서 고기를 굽고, 음료수는 기계가, 감자튀김은 튀김기가

### Thread

- [ ]  **쓰레드** : 하나의 프로세스내에서 돌아가는 병행적인 메소드
- 쓰레드는 프로세스내에서 Stack영역만 따로 할당받고 Code, Data, Heap영역은 공유한다.  즉, 프로세스내의 여러자원들을 공유하면서 실행된다.
- 모든 자바어플리케이션은 Main Thread가 main()메소드를 실행하면서 시작한다.
    - 멀티 쓰레드의 장점 : 시스템자원의 효율성 증대, 처리량 증가, 응답시간 단축, 통신의 부담 감소
    - 멀티 쓰레드의 단점 : 주의깊은 설계, 까다로운 디버깅, 동기화문제, 하나의 쓰레드가 잘못되어도 프로그램이 멈춤
- 멀티 프로세스 대신 멀티쓰레드를 사용하는 이유
- 위에서 말한 쓰레드의 장점.

- [ ]  **생성방법 2가지**
  1. Thread상속  (java.lang.Thread)
  2. Runnable 인터페이스를 구현

- [ ]  **대표적인 메소드**
- sleep, start, join, run 이 있다.
- 호출시 실행하는 메소드는 **start**해주지만 쓰레드가 실제 돌아갈때는 오버라이드하는 run이 돌아간다.
- run을 통해 실행시키면 stack으로 쌓여서 병행처리가 안된다. 해당메소드가 종료되어야 다른 스레드가 실행된다.
- start를 통해 실행해야 정상적인 병행처리가 된다.
- 쓰레드를 start하면 바로 실행하는것이 아니라 실행대기상태에 있따가 OS의 스케쥴러가 작성한 스케줄에 의해 순서대로 자기 차례에 실행되는 구조다.
- 쓰레드의 상태 6가지. getState()를 하면 알 수 있다.
    - NEW
    - RUNNABLE
    - BLOCKED
    - WAITING
    - TIMED_WAITING
    - TERMINATED
    
- [ ]  쓰레드의 종료
- 쓰레드는 자신의 run메소드가 모두 실행되면 자동적으로 종료된다.
- 그런데 run메소드의 끝까지 가기전에 '즉시 종료' 해야한다면 boolean으로 된 플래그를 사용하거나 interrupt()메소드를 이용하는 방법이 있다
- interrupt() 메소드는 InterruptedException 예외를 발생시키는데, 주의해야할점은 interrupt메소드를 이용하기위해서는 종료시키고 싶은 메소드가 일시정지상태일때 정지된다는것이다.
- 돌아가고있는 중에서는 정지가 안된다.

### 실습 - Thread

- Runnable 인터페이스 사용
- checkThread.java
    
    ```java
    public class checkThread implements Runnable {
    	String name;
    	
    	public checkThread(String name) {
    		this.name = name;
    	}	
    	
    	@Override
    	public void run() {
    		for(int i=0; i<5; i++) {
    			try {
    				System.out.println(name);
    				Thread.sleep(1000); // 1000 밀리세컨드 == 1초
    			} catch (InterruptedException e) {
    				// TODO Auto-generated catch block
    				e.printStackTrace();
    			}
    		}
    		System.out.println(name + "쓰레드 종료");
    	}
    
    }
    ```
    
- Main.java
    
    ```java
    public class Main {
    
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		
    		Runnable d1 = new checkThread("피카츄"); // 다형성
    		Runnable d2 = new checkThread("꼬부기");
    		Runnable d3 = new checkThread("파이리");
    		Runnable d4 = new checkThread("롱스톤");
    		
    		Thread thread1 = new Thread(d1);
    		Thread thread2 = new Thread(d2);
    		Thread thread3 = new Thread(d3);
    		Thread thread4 = new Thread(d4);
    		
    		thread1.start();
    		thread2.start();
    		thread3.start();
    		thread4.start();
    
    	}
    }
    ```
    
- 코드 실행시 4개의 쓰레드 순서가 바뀌기도 한다

![Untitled](/images/Java_thread/Untitled.png)

### 실습 - Thread 타이머

- **시간을 이용한 프로그래밍**
- < 5판 3선승제 -  컴퓨터와 가위바위보 게임>
- 이겼다 / 졌다 판단해서 출력
- 위의 개발에다가 방금 배운 쓰레드로 타이머 만들기 원래는 사용자의 입력을 받을때까지 아무작업 안하고 기다렸는데 멀티쓰레드로 타이머가 돌아가면서 3초 안에 입력 안하면 지게 만들기
- Thread 클래스 상속하여 사용

- [ ]  정답지
- GameControl.java
    
    ```java
    import java.util.Scanner;
    
    public class GameControl {
    
    	public static boolean inputCheck = false;	//유저가 입력 했는지
    	
    	static int life = 999;			//남은목숨. 컴퓨터가 이기면 1감소
    	static int totalGameCount = 1;	//총 게임진행횟수
    	static int win=0;				//유저의 승리횟수
    	static int draw=0;				//비김
    	static int lose=0;				//유저의 패배횟수
    	
    	public static void main(String[] args) {
    		GameTimer timer = null;
    		GameControl gc = new GameControl();
    		String computersChoice = null;	//컴퓨터의 선택
    		String usersChoice = null;   // 유저의 선택
    		
    		// 난수를 이용하여 컴퓨터의 가위 바위 보를 정한다.
    		String[] data = {"가위", "바위", "보"};
    		
    		while(win<3 && lose<3) {	//누구 하나라도 해당횟수의 승리를 하게되면 중단
    			timer = new GameTimer(totalGameCount);	//게임진행횟수를 인자로줌. 매번 새로운 타이머 생성
    			timer.start();
    			usersChoice = gc.choiceRSP();	//유저입력 true로 바꾸는 작업도 안에서 한다.
    			computersChoice = data[(int) (Math.random()*3)];  //0.000001~2.9999999니까 0,1,2
    			System.out.println("\n"+gc.judge(usersChoice,computersChoice));
    			gc.showScore();
    			totalGameCount++;
    		}
    		gc.printGameOver();
    
    	}
    	
    	//유저에게 가위바위보중 하나를 입력받도록 한다.
    		public String choiceRSP() {
    			System.out.println("\n****가위, 바위, 보 중 무엇을 내겠습니까?****");
    			Scanner sc = new Scanner(System.in);
    			String result = sc.nextLine();
    			if(!result.equals("가위") && !result.equals("바위") && !result.equals("보")) {
    				System.out.println("가위바위보 중에 하나를 입력해주세요.");
    			}else {
    				inputCheck = true;  // 정상적인 가위바위보를 냈을때 입력이 완료로 변경
    			}
    			return result;
    		}
    		 
    		//결과 판단하기
    		public String judge(String usersChoice, String computersChoice) {
    			System.out.printf("당신은 %s를 내고 컴퓨터는 %s를 냈습니다.", usersChoice, computersChoice);
    			inputCheck = false;	//이것이 핵심이였음!!!!!!!!!!!!
    			if( usersChoice.equals(computersChoice) ){
    				draw++;
    				return "비김";
    			}else if( (usersChoice.equals("가위") && computersChoice.equals("보"))
    					 || (usersChoice.equals("바위") && computersChoice.equals("가위"))
    					 || (usersChoice.equals("보") && computersChoice.equals("바위")) ){
    				win++;
    				return "승리";
    			}else{
    				life--;
    				lose++;
    				return "패배";
    			}
    		}
    		
    		public void showScore() {
    			System.out.printf("총%s판(%d승 %d무 %d패)\n", totalGameCount, win, draw, lose);
    		}
    		
    		public void printGameOver() {
    			System.out.println("게임이 끝났습니다.");
    			if(win>lose) {
    				System.out.println("당신이 이겼습니다.");
    			}else {
    				System.out.println("컴퓨터가 이겼습니다.");
    			}
    		}
    }
    ```
    
- GameTimer.java
    
    ```java
    
    public class GameTimer extends Thread{
    	int gameCount=0;
    	public GameTimer(int now) {	//몇번째 게임에 만들어진 타이머인가
    		super();
    		this.gameCount = now;
    	}
    	
    	@Override
    	public void run() {
    		for(int i=5; i>=1; i--){
    			/* 여러번 경기를 할때 어려움이 발생하는 지점 
    			 * inputCheck를 true로 하면 다음 타이머 작동안하고,
    			 * false로 하면 이전것이 살아있어서 남아있는 초를 출력하게 된다.
    			 * 타이머는 5초를 셀 뿐이다. 타이머의 제어는 타이머의 외부에서 일어나도록 하자. 객체지향적으로
    			 */
    
    			if(GameControl.inputCheck==true || gameCount!=GameControl.totalGameCount){
    				//유저가 입력했거나  타이머가 자동한게임회차와 본게임의 회차가 다르면
    				return;	//run함수를 나가버리면 쓰레드는 자신이 가지고있는 자원을 정상적으로 반납하며 종료된다.
    			}
    			try {
    				System.out.println(i);	//타임 출력
    				Thread.sleep(1000);
    			} catch (InterruptedException e) {
    				e.printStackTrace();
    			}
    		}
    		//System.exit(0);	//타이머가 끝났다고 시스템이 끝나면안되지.
    		System.out.println(this.getName()+" 시간초과");
    	}
    }
    ```
    

- [ ]  나의 풀이
- 단, GameTimer는 그대로 사용
- Main.java
    
    ```java
    import java.util.Random;
    import java.util.Scanner;
    import java.util.Timer;
    import java.util.TimerTask;
    
    public class Main {
    	public static boolean inputCheck = false;
    	static int totalGameCount = 1;
    	static int win=0;
    	static int lose=0;
    	static int draw=0;
    	static int select=10;
    	static int count=0;
    	static int rand=0;
    	
    	public static void main(String[] args) {
    		// TODO Auto-generated method stub
    		GameTimer timer = null;
    		Main gc = new Main();
    		System.out.println("게임을 시작합니다.");
    		Random random = new Random();
    		
    		while(win<3 && lose<3) {
    			
    			timer = new GameTimer(totalGameCount);	//게임진행횟수를 인자로줌. 매번 새로운 타이머 생성
    			timer.start();
    			select = gc.choiceRSP();	//유저입력 true로 바꾸는 작업도 안에서 한다.
    			rand =random.nextInt(3)+1;
    			gc.judge(select, rand);
    
    			totalGameCount++;
    		}
    
    		matchResult();
    	}
    
    	public int choiceRSP() {
    		System.out.printf("1. 가위 \n2. 바위\n3. 보\n");
    		System.out.printf("선택지 중에서 하나를 선택해주세요 : ");
    		Scanner scanner = new Scanner(System.in);
    		select = scanner.nextInt();
    		return select;
    	}
    	
    	public void judge(int select, int a) {
    		
    		inputCheck = false;	//이것이 핵심이였음!!!!!!!!!!!!
    		String pc="";
    		String me="";
    		String[] arr = {"scissor", "rock", "paper"};
    		me = arr[select-1];
    		pc = arr[a-1];
    		System.out.println("==============");
    		System.out.println("나 : " + me);
    		System.out.println("컴퓨터 : " + pc);
    		
    		switch(select-1) {
    		case 0:
    			if(pc==arr[1]) {
    				System.out.println("결과 : 패배");
    				lose++;
    			}else if(pc==arr[2]) {
    				System.out.printf("결과 : 승리!!!  >  %d승\n", ++win);
    			}else {
    				System.out.println("결과 : 무승부");
    			}
    			break;
    		case 1:
    			if(pc==arr[0]) {
    				System.out.printf("결과 : 승리!!!  >  %d승\n", ++win);
    			}else if(pc==arr[2]) {
    				System.out.println("결과 : 패배");
    				lose++;
    			}else {
    				System.out.println("결과 : 무승부");
    			}
    			break;
    		case 2:
    			if(pc==arr[0]) {
    				System.out.println("결과 : 패배");
    				lose++;
    			}else if(pc==arr[1]) {
    				System.out.printf("결과 : 승리!!!  >  %d승\n", ++win);
    			}else {
    				System.out.println("결과 : 무승부");
    			}
    			break;
    		default:
    			break;
    		}
    		System.out.println("==============");
    	}
    	
    	static public void matchResult() {
    		System.out.println("==============");
    		System.out.println("==============");
    		System.out.printf("최종 전적 : %d승 / %d패\n", win, lose);
    	}
    }
    ```
    
- GameTimer.java
    
    ```java
    public class GameTimer extends Thread{
    	int gameCount=0;
    	
    	
    	public GameTimer(int now) {	//몇번째 게임에 만들어진 타이머인가
    		super();
    		this.gameCount = now;
    	}
    	
    	@Override
    	public void run() {
    		for(int i=5; i>=1; i--){
    			/* 여러번 경기를 할때 어려움이 발생하는 지점 
    			 * inputCheck를 true로 하면 다음 타이머 작동안하고,
    			 * false로 하면 이전것이 살아있어서 남아있는 초를 출력하게 된다.
    			 * 타이머는 5초를 셀 뿐이다. 타이머의 제어는 타이머의 외부에서 일어나도록 하자. 객체지향적으로
    			 */
    
    			if(Main.inputCheck==true || gameCount!=Main.totalGameCount){
    				//유저가 입력했거나  타이머가 자동한게임회차와 본게임의 회차가 다르면
    				return;	//run함수를 나가버리면 쓰레드는 자신이 가지고있는 자원을 정상적으로 반납하며 종료된다.
    			}
    			try {
    				System.out.println(i);	//타임 출력
    				Thread.sleep(1000);
    			} catch (InterruptedException e) {
    				e.printStackTrace();
    			}
    		}
    		//System.exit(0);	//타이머가 끝났다고 시스템이 끝나면안되지.
    		System.out.println(this.getName()+" 시간초과");
    	}
    }
    ```