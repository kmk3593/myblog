---
title: "JPA 영속석 컨텍스트"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-06-12'
---

# 영속성 컨텍스트

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****

---

### JPA에서 가장 중요한 2가지

- 객체와 관계형 데이터베이스 매핑하기 (Object Relational Mapping)
- 영속성 컨텍스트

### 엔티티 매니저 펙토리와 엔티티 매니저

![Untitled](/images/jpa_em/Untitled.png)

### 영속성 컨텍스트

- JPA를 이해하는데 가장 중요한 용어
- “**엔티티를 영구 저장하는 환경**”이라는 뜻
- `EntityManager.persist(entity);`

### 엔티티의 생명주기

- **비영속 (new/transient)**
영속성 컨텍스트와 전혀 관계가 없는 새로운 상태

- **영속 (managed)**
영속성 컨텍스트에 관리되는 상태

- **준영속 (detached)**
영속성 컨텍스트에 저장되었다가 분리된 상태

- **삭제 (removed)**
삭제된 상태

## 영속

- **Entity Manager 안에 담은 상태**

![Untitled](/images/jpa_em/Untitled%201.png)

## 비영속

- **Entity Manager 안에 담지 않은 상태**

![Untitled](/images/jpa_em/Untitled%202.png)

### DB에 저장되는 시점

- `persist(member)` 하더라도 DB에 저장되지 않는다.
- `tx.commit( );`
    - **Transaction Commit 실행 후에서야 저장**된다

### 준영속, 삭제

- detach( ) 사용한 상태?
- delete( ) 사용한 상태?

```jsx
//**회원 엔티티를 영속성 컨텍스트에서 분리, 준영속 상태**
em.detach(member);

//**객체를 삭제한 상태(삭제)**
em.remove(member);
```

### 영속성 컨텍스트의 이점

- 1차 캐시
- 동일성(identity) 보장
- 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)
- 변경 감지(Dirty Checking)
- 지연 로딩(Lazy Loading)

### 이점 1 : 1차 캐시

- DB까지 가지 않고 값을 가져 올 수 있는 경우가 있다

![Untitled](/images/jpa_em/Untitled%203.png)

![Untitled](/images/jpa_em/Untitled%204.png)

---

### 이점 2 : 영속 엔티티의 동일성 보장

- 1차 캐시로 반복 가능한 읽기(REPEATABLE READ) 등급의 트랜잭션 격리 수준을 데이터베이스가 아닌 애플리케이션 차원에서 제공

```jsx
Member a = em.find(Member.class, "**member1**");
Member b = em.find(Member.class, "**member1**");

System.out.println(**a == b**); //동일성 비교 **true**
```

---

### 이점 3 : 엔티티 등록 트랜잭션을 지원하는 쓰기 지연

- 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)

```jsx
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = em.getTransaction();
//엔티티 매니저는 데이터 변경시 트랜잭션을 시작해야 한다.

transaction.begin(); // [트랜잭션] 시작
em.persist(memberA);
em.persist(memberB);
//여기까지 INSERT SQL을 데이터베이스에 보내지 않는다.
//커밋하는 순간 데이터베이스에 INSERT SQL을 보낸다.

transaction.commit(); // [트랜잭션] 커밋
```

- member1, member2 있을 경우,  하나씩 차례로 작업한다

![Untitled](/images/jpa_em/Untitled%205.png)

---

### 이점 4 : 엔티티 수정 변경 감지 (Dirty Checking)

```jsx
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = em.getTransaction();
transaction.begin(); // [트랜잭션] 시작

// 영속 엔티티 조회
Member memberA = em.find(Member.class, "memberA");

// 영속 엔티티 데이터 수정
memberA.setUsername("hi");
memberA.setAge(10);
//em.update(member) 이런 코드가 있어야 하지 않을까?

transaction.commit(); // [트랜잭션] 커밋
```

- **엔티티 vs 스냅샷**
- 값을 비교하여 수정되었는지 확인한다

![Untitled](/images/jpa_em/Untitled%206.png)

---

### 이점 5 : 플러시

- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영하는 것

- 플러시 발생
    - 변경 감지
    - 수정된 엔티티 쓰기 지연 SQL 저장소에 등록
    - 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
    (등록, 수정, 삭제 쿼리)

- 영속성 컨텍스트를 플러시하는 방법

```jsx
em.flush() - 직접 호출 

트랜잭션 커밋 - 플러시 자동 호출 

JPQL 쿼리 실행 - 플러시 자동 호출
```

### JPQL 쿼리 실행 시 플러시가 자동으로 호출되는 이유

- 

```jsx
em.persist(memberA);
em.persist(memberB);
em.persist(memberC);
//중간에 JPQL 실행
query = em.createQuery("select m from Member m", Member.class);
List<Member> members= query.getResultList();
```

### 플러시는!

- 영속성 컨텍스트를 비우지 않음
- 영속성 컨텍스트의 변경내용을 데이터베이스에 동기화
- 트랜잭션이라는 작업 단위가 중요 -> 커밋 직전에만 동기화하면 됨

---

### 준영속

- 영속 -> 준영속
- 영속 상태의 엔티티가 영속성 컨텍스트에서 분리 **(detached)**
- 영속성 컨텍스트가 제공하는 기능을 사용 못함

### 준영속 상태로 만드는 방법

- `em.detach(entity)`
특정 엔티티만 준영속 상태로 전환

- `em.clear()`
영속성 컨텍스트를 완전히 초기화

- `em.close()`
영속성 컨텍스트를 종료