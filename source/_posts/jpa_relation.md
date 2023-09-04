---
title: "JPA 프록시, 연관 관계"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-07-17'
---

# 프록시, 연관 관계

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****

---

## 프록시

---

**Member를 조회할 때 Team도 함께 조회해야 할까?**

![Untitled](/images/jpa_relation/Untitled.png)

- 회원과 팀 함께 출력

```jsx
public void printUserAndTeam(String memberId) {
	 Member member = em.find(Member.class, memberId);
		 Team team = member.getTeam();
		 System.out.println("회원 이름: " + member.getUsername());
		 System.out.println("소속팀: " + team.getName()); 
	}
```

- 회원만 출력

```jsx
public void printUser(String memberId) {
	 Member member = em.find(Member.class, memberId);
		 Team team = member.getTeam();
		 System.out.println("회원 이름: " + member.getUsername());
	}
```

### 프록시 기초

- **em.find()**  **vs**  **em.getReference()**
- em.find()
    - 데이터베이스를 통해서 **실제 엔티티 객체 조회**
- em.getReference()
    - 데이터베이스 조회를 미루는 **가짜(프록시) 엔티티 객체 조회**

- Proxy가 생성한 가짜 객체

![Untitled](/images/jpa_relation/Untitled%201.png)

### 프록시 특징

![Untitled](/images/jpa_relation/Untitled%202.png)

### 프록시 특징

- 프록시 객체는 실제 객체의 참조(target)를 보관
- 프록시 객체를 호출하면 프록시 객체는 실제 객체의 메소드 호출

![Untitled](/images/jpa_relation/Untitled%203.png)

### 프록시 초기화

```jsx
Member member = em.**getReference**(Member.class, “id1”);
member.getName();
```

![Untitled](/images/jpa_relation/Untitled%204.png)

### 프록시 특징

- 프록시 객체는 처음 사용할 때 **한 번만 초기화**
- 프록시 객체를 초기화 할 때, **프록시 객체가 실제 엔티티로 바뀌는 것은 아님**
    - 초기화되면 프록시 객체를 통해서 실제 엔티티에 **접근만 가능**
- 프록시 객체는 원본 엔티티를 상속 받음, 따라서 타입 체크시 주의해야 함
    - (**== 비교 실패**, 대신 **instance of 사용**)
- 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 **em.getReference()** 호출해도 실제 엔티티 반환
- 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태일 때, 프록시를 초기화하면 문제 발생
    - 하이버네이트는 org.hibernate.LazyInitializationException 예외를 터트림

### 프록시 확인

- 프록시 인스턴스의 초기화 여부 확인
**PersistenceUnitUtil.isLoaded(Object entity)**
- 프록시 클래스 확인 방법
**entity.getClass().getName() 출력(..javasist.. or HibernateProxy…)**
- 프록시 강제 초기화
**org.hibernate.Hibernate.initialize(entity);**
- 참고: JPA 표준은 강제 초기화 없음
강제 호출: **member.getName()**

---

## 즉시 로딩과 지연 로딩

- 프록시를 활용한다

### Member를 조회할 때 Team도 함께 조회해야 할까?

- 단순히 member 정보만 사용하는 비즈니스 로직
**println(member.getName());**

![Untitled](/images/jpa_relation/Untitled%205.png)

### 지연 로딩 LAZY을 사용해서 프록시로 조회

```jsx
@Entity
 public class Member {
	 @Id
	 @GeneratedValue
	 private Long id;

	 @Column(name = "USERNAME")
	 private String name;

	 @ManyToOne(fetch = FetchType.**LAZY**) //**
	 @JoinColumn(name = "TEAM_ID")
	 private Team team;
	 ..
}
```

### 지연로딩

![Untitled](/images/jpa_relation/Untitled%206.png)

### 지연 로딩 LAZY을 사용해서 프록시로 조회

- 코드

```jsx
**Member member = em.find(Member.class, 1L);**
```

![Untitled](/images/jpa_relation/Untitled%207.png)

- 코드

```jsx
**Team team = member.getTeam();
team.getName(); // 실제 team을 사용하는 시점에 초기화(DB 조회)**
```

![Untitled](/images/jpa_relation/Untitled%208.png)

### 즉시 로딩

- 가급적 사용하지 말 것
- EAGER 가 보인다면 ‘즉시 로딩’
    - 거기에 더해 N:1, 1:1 의 경우도 기본이 ‘즉시 로딩’

- 즉시 로딩 EAGER 를 사용해서 함께 조회

```jsx
@Entity
 public class Member {
 @Id
 @GeneratedValue
 private Long id;
 @Column(name = "USERNAME")
 private String name;
 @ManyToOne(fetch = FetchType.**EAGER**) //**
 @JoinColumn(name = "TEAM_ID")
 private Team team;
 .
}
```

![Untitled](/images/jpa_relation/Untitled%209.png)

### 프록시와 즉시 로딩 주의

- **가급적 지연 로딩만 사용**(특히 실무에서)
- 즉시 로딩을 적용하면 예상하지 못한 SQL이 발생
- **즉시 로딩은 JPQL에서 N+1 문제**를 일으킨다.
- @ManyToOne, @OneToOne은 **기본이 즉시 로딩**
-> **LAZY로 설정**
- @OneToMany, @ManyToMany는 기본이 지연 로딩

![Untitled](/images/jpa_relation/Untitled%2010.png)

---

## 영속성 전이 : CASCADE

- 특정 엔티티를 영속 상태로 만들 때 **연관된 엔티티도 함께 영속 상태로** 만들도 싶을 때
• 예: 부모 엔티티를 저장할 때 자식 엔티티도 함께 저장

![Untitled](/images/jpa_relation/Untitled%2011.png)

### 영속성 전이 : 저장

```jsx
@OneToMany(mappedBy="parent", cascade=CascadeType.PERSIST)
```

![Untitled](/images/jpa_relation/Untitled%2012.png)

### 영속성 전이: CASCADE - 주의!

- 영속성 전이는 연관 관계를 **매핑하는 것과 아무 관련이 없음**
- 엔티티를 영속화할 때 **연관된 엔티티도 함께 영속화하는 편리함**을 제공할 뿐

### CASCADE의 종류

- **ALL**: 모두 적용
- **PERSIST**: 영속
- **REMOVE**: 삭제
- MERGE: 병합
- REFRESH: REFRESH
- DETACH: DETACH

### 고아 객체

- **고아 객체 제거**: 부모 엔티티와 **연관 관계가 끊어진 자식 엔티티를 자동으로 삭제**
- orphanRemoval = true
- Parent parent1 = em.find(Parent.class, id);
    
    parent1.getChildren().remove(0);
    
    //자식 엔티티를 컬렉션에서 제거
    
- DELETE FROM CHILD WHERE ID=?

### 고아 객체 - 주의

- **참조가 제거된 엔티티**는 다른 곳에서 참조하지 않는 **고아 객체로 보고 삭제**하는 기능
- 참조하는 곳이 하나일 때 사용해야 함!
- 특정 엔티티가 개인 소유할 때 사용
- @OneToOne, @OneToMany만 가능
- 참고 : 개념적으로 부모를 제거하면 자식은 고아가 된다. 따라서 고아 객체 제거 기능을 활성화 하면, 부모를 제거할 때 자식도 함께 제거된다.
- 이것은 CascadeType.REMOVE처럼 동작한다.