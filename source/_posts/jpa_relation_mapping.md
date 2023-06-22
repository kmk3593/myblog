---
title: "JPA 연관 관계 매핑"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-06-22'
---

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****

---

### 학습 목표

- 객체와 테이블 연관 관계의 차이를 이해
- 객체의 참조와 테이블의 외래 키를 매핑

### 용어 이해

- 방향(Direction): 단방향, 양방향
- 다중성(Multiplicity)
    - 다대일(N:1)
    - 일대다(1:N)
    - 일대일(1:1)
    - 다대다(N:M)
- 연관 관계의 주인**(Owner)** : 객체 양방향 **연관 관계는 관리 주인이 필요**

### 연관 관계가 필요한 이유

- **객체 지향 설계의 목표**는 **자율적인 객체들의 협력 공동체**를 만드는 것이다.

- 예제 시나리오
    - 회원과 팀이 있다.
    - 회원은 하나의 팀에만 소속될 수 있다.
    - 회원과 팀은 다대일 관계다

- 객체를 테이블에 맞추어 모델링

![Untitled](/images/jpa_relation_mapping/Untitled.png)

---

객체를 테이블에 맞추어 데이터 중심으로 모델링하면**,
협력 관계를 만들 수 없다**

---

### 객체 지향 모델링 (객체 연관 관계 사용)

![Untitled](/images/jpa_relation_mapping/Untitled%201.png)

### 객체 지향 모델링

- 객체의 참조와 테이블의 외래 키를 매핑
- 코드 예시

```jsx
@Entity
public class Member { 

		@Id 
		@GeneratedValue
		private Long id;

		@Column(name = "USERNAME")
		private String name;

		private int age;

		// 다대일 관계
		// 외래키 키 매핑
		@ManyToOne
		@**JoinColumn**(name = "TEAM_ID")
		private Team team;
```

- 객체 지향 모델링

![Untitled](/images/jpa_relation_mapping/Untitled%202.png)

- 연관 관계 저장

```jsx
//팀 저장
 Team team = new Team();
 team.setName("TeamA");
 em.persist(team);

 //회원 저장
 Member member = new Member();
 member.setName("member1");
 member.setTeam(team); //단방향 연관관계 설정, 참조 저장
 em.persist(member);
```

---

## 양방향 연관 관계와 연관 관계의 주인

- 양방향 매핑

![Untitled](/images/jpa_relation_mapping/Untitled%203.png)

- 양방향 매핑
- Member 엔티티는 단방향과 동일

```jsx
@Entity
 public class Member { 
		 @Id 
		 @GeneratedValue
		 private Long id;

		 @Column(name = "USERNAME")
		 private String name;

		 private int age;

		 // 키 매핑
		 @ManyToOne
		 @JoinColumn(name = "TEAM_ID")
		 private Team team;
```

- (Team 엔티티는 컬렉션 추가)
- mappedBy 사용

```jsx
@Entity
 public class Team {
		 @Id
		 @GeneratedValue
		 private Long id;
		 
	   private String name;

		 @OneToMany(**mappedBy** = "team")
		 List<Member> members = new ArrayList<Member>();
		 … 
		 }
```

- 양방향 매핑
- 반대 방향으로 객체 그래프 탐색

```jsx
//조회
 Team findTeam = em.find(Team.class, team.getId()); 
 int memberSize = findTeam.getMembers().size(); //역방향 조회
```

### 객체와 테이블이 관계를 맺는 차이

![Untitled](/images/jpa_relation_mapping/Untitled%204.png)

### 객체와 테이블이 관계를 맺는 차이

![Untitled](/images/jpa_relation_mapping/Untitled%205.png)

- 객체의 **양방향** 관계는 사실 **양방향 관계가 아니라 서로 다른 단뱡향 관계 2개**다.
- 객체를 양방향으로 참조하려면 단방향 연관 관계를 2개 만들어야 한다

![Untitled](/images/jpa_relation_mapping/Untitled%206.png)

- 테이블은 *외래 키 하나로 두 테이블의 연관* 관계를 관리
- MEMBER.TEAM_ID **외래 키 하나로 양방향 연관 관계 가짐**
(**양쪽으로 조인**할 수 있다.)

```jsx
SELECT * 
FROM **MEMBER** M
JOIN **TEAM** T ON M.TEAM_ID = T.TEAM_ID 

SELECT * 
FROM TEAM T
JOIN **MEMBER** M ON T.TEAM_ID = M.TEAM_ID
```

- 둘 중 하나로 외래 키를 관리해야 한다
- 둘 중 외래키를 관리하는 쪽이 주인(= Owner)

![Untitled](/images/jpa_relation_mapping/Untitled%207.png)

### 누구를 주인으로?

- **외래 키가 있는 있는 곳**을 주인으로 정해야 한다
- 여기서는 Member.team이 연관 관계의 주인

![Untitled](/images/jpa_relation_mapping/Untitled%208.png)

### 양방향 매핑시 가장 많이 하는 실수

- 연관 관계의 주인에 값을 입력하지 않음

```jsx
Team team = new Team();
team.setName("TeamA");
em.persist(team);

Member member = new Member();
member.setName("member1");
//역방향(주인이 아닌 방향)만 연관관계 설정
team.getMembers().add(member);
em.persist(member);
```

![Untitled](/images/jpa_relation_mapping/Untitled%209.png)

### 양방향 매핑시 연관 관계의 주인에 값을 입력해야 한다.

- 순수한 객체 관계를 고려하면 **항상 양쪽다 값을 입력**해야 한다.

```jsx
Team team = new Team();
team.setName("TeamA");
em.persist(team);

Member member = new Member();
member.setName("member1");
team.getMembers().add(member); 

//연관관계의 주인에 값 설정
member.setTeam(team); //**
em.persist(member);
```

![Untitled](/images/jpa_relation_mapping/Untitled%2010.png)

### 눈에 띄게 변경하는 법

- settter 함수를 사용하면 되지만
- 좀 더 의도를 드러내면서 바꿀 방법이다
    - 다음과 같이 간단한 함수를 만들어서 사용하면 된다

```jsx
public void changeTeam(Team team) {
        this.team = team;
        team.getMembers().add(this);
    }
```

### 양방향 연관 관계 주의

- 순수 객체 상태를 고려해서 항상 양쪽에 값을 설정하자
- 연관 관계 편의 메소드를 생성하자
- 양방향 매핑 시에 무한 루프를 조심하자
    - 예: toString(), lombok, JSON 생성 라이브러리

### 양방향 매핑 정리

- **단방향 매핑 만으로도 이미 연관 관계 매핑은 완료**
    - 보통은 단방향 매핑만 해도 충분하다
- 양방향 매핑은 반대 방향으로 조회(객체 그래프 탐색) 기능이 추가된 것 뿐
- JPQL에서 역방향으로 탐색할 일이 많음
- 단방향 매핑을 잘 하고 양방향은 필요할 때 추가해도 됨
    - 테이블에 영향을 주지 않음

---

## 다양한 연관 관계 매핑

### 연관 관계 매핑시 고려 사항 3가지

- 다중성
- 단방향, 양방향
- 연관 관계의 주인

### 다중성

- 다대일: @ManyToOne
- 일대다: @OneToMany
- 일대일: @OneToOne

- 다대다: @ManyToMany
    - 이건 **실무에서 사용금지**

**테이블**

- 외래 키 하나로 양쪽 조인 가능
- 사실 방향이라는 개념이 없음

**객체**

- 참조용 필드가 있는 쪽으로만 참조 가능
- 한쪽만 참조하면 단방향
- 양쪽이 서로 참조하면 양방향

### 연관관계의 주인

- 테이블은 **외래 키 하나**로 두 테이블이 연관 관계를 맺음
- 객체 양방향 관계는 A->B, B->A 처럼 **참조가 2군데**
- 객체 양방향 관계는 참조가 2군데 있음. 둘 중 테이블의 외래 키를 관리할 곳을 지정해야 함
- 연관 관계의 주인
    - 외래 키를 관리하는 참조
- 주인의 반대편
    - 외래 키에 영향을 주지 않음, 단순 조회만 가능

### 다 대 일 [N : 1]

- 다대일 단방향
- 앞글자가 관계의 주인 (Owner)이므로
- 다(N) 쪽이 주인이다
    - 그리고 FK가 있는 쪽이다

![Untitled](/images/jpa_relation_mapping/Untitled%2011.png)

- 다대일 양방향
- 앞글자가 관계의 주인 (Owner)이므로
- 다(N) 쪽이 주인이다
    - 그리고 FK가 있는 쪽이다

![Untitled](/images/jpa_relation_mapping/Untitled%2012.png)

### 다 대 일 정리

- **외래 키가 있는 쪽**이 연관 관계의 **주인**
- 양쪽을 서로 참조하도록 개발

---

### 일 대 다 [1 : N]

- 일대다 단방향
- 일(1) 쪽이 관계의 주인이다

![Untitled](/images/jpa_relation_mapping/Untitled%2013.png)

### 정리

- 일대다 단방향은 일대다(1:N)에서 일(1)이 연관관계의 주인
- 테이블 일대다 관계는 항상 다(N) 쪽에 외래 키가 있음
- 객체와 테이블의 차이 때문에 반대편 테이블의 외래 키를 관리하는 특이한 구조
- @JoinColumn을 꼭 사용해야 함.
    - 그렇지 않으면 조인 테이블 방식을 사용함  (중간에 테이블을 하나 추가함)

### 일 대 다 단방향 정리

- 일대다 단방향 매핑의 단점
- 엔티티가 관리하는 외래 키가 다른 테이블에 있음
- 연관 관계 관리를 위해 추가로 UPDATE SQL 실행
- 일대다 단방향 매핑 보다는 다대일 양방향 매핑을 사용하자

### 일 대 다 양방향

- 이런 매핑은 **공식적으로 존재 X**

![Untitled](/images/jpa_relation_mapping/Untitled%2014.png)

### 일 대 다 양방향 정리

- 이런 매핑은 공식적으로 존재X
- @JoinColumn(insertable=false, updatable=false)
- 읽기 전용 필드를 사용해서 양방향 처럼 사용하는 방법
- **다대일 양방향을 사용**하자

---

## 일 대 일 관계 [1 : 1]

### 일 대 일 단방향

- 일대일 관계는 그 반대도 일대일
- 주 테이블이나 대상 테이블 중에 외래 키 선택 가능
- 주 테이블에 외래 키
- 대상 테이블에 외래 키
- 외래 키에 데이터베이스 유니크(UNI) 제약 조건 추가

- 다대일(@ManyToOne) 단방향 매핑과 유사

![Untitled](/images/jpa_relation_mapping/Untitled%2015.png)

### 일 대 일 양방향

- 다대일 양방향 매핑처럼 외래 키가 있는 곳이 연관관계의 주인
- 반대편은 mappedBy 적용

![Untitled](/images/jpa_relation_mapping/Untitled%2016.png)

### 일대일: 대상 테이블에 외래 키 단방향

![Untitled](/images/jpa_relation_mapping/Untitled%2017.png)

### 일대일: 대상 테이블에 외래 키 단방향 정리

- 단방향 관계는 JPA 지원X
- 양방향 관계는 지원

### 일대일: 대상 테이블에 외래 키 양방향

- 사실 일대일 주 테이블에 외래 키 양방향과 매핑 방법은 같음

![Untitled](/images/jpa_relation_mapping/Untitled%2018.png)

### 일 대 일 정리

- **주 테이블에 외래 키**
    - 주 객체가 대상 객체의 참조를 가지는 것 처럼
    주 테이블에 외래 키를 두고 대상 테이블을 찾음
    - 객체지향 개발자 선호
    - JPA 매핑 편리
    - 장점: 주 테이블만 조회해도 대상 테이블에 데이터가 있는지 확인 가능
    - 단점: 값이 없으면 외래 키에 null 허용
- **대상 테이블에 외래 키**
    - 대상 테이블에 외래 키가 존재
    - 전통적인 데이터베이스 개발자 선호
    - 장점: 주 테이블과 대상 테이블을 일대일에서 일대다 관계로 변경할 때 테이블 구조 유지
    - 단점: 프록시 기능의 한계로 지연 로딩으로 설정해도 항상 즉시 로딩됨
        
               (프록시는 뒤에서 설명)
        

---

## 다 대 다

- 실무에서 사용 X
- 관계형 데이터베이스는 정규화된 테이블 2개로 다대다 관계를 표현 불가능
- 연결 테이블을 추가해서 일대다, 다대일 관계로 풀어내야함

![Untitled](/images/jpa_relation_mapping/Untitled%2019.png)

### 정리

- 편리해 보이지만 실무에서 사용X
- 연결 테이블이 단순히 연결만 하고 끝나지 않음
- 주문시간, 수량 같은 데이터가 들어올 수 있음

---

### @JoinColumn

- 외래 키를 매핑할 때 사용

![Untitled](/images/jpa_relation_mapping/Untitled%2020.png)

### @ManyToOne - 주요 속성

- 다대일 관계 매핑

![Untitled](/images/jpa_relation_mapping/Untitled%2021.png)

### @OneToMany - 주요 속성

- 일대다 관계 매핑

![Untitled](/images/jpa_relation_mapping/Untitled%2022.png)