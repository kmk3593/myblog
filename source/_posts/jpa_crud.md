---
title: "JPA CRUD"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-06-07'
---
### = INSERT, SELECT, UPDATE, DELETE

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****

---

### INSERT

- persist( ) 사용

```jsx
package com.hellojpa;

import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;

public class JpaMain {
    public static void main(String[] args) {

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("JPABOOK");

        EntityManager em = emf.createEntityManager();

        // 트랜잭션
        EntityTransaction tx = em.getTransaction();
        tx.begin();

        try {
            Member member = new Member();
            member.setId(1L);
            member.setName("HelloA");

            // member 인스턴스에 들어있는 값을 em에 저장하다 = db에 삽입하다
            em.persist(member);

						tx.commit();
        } catch (Exception e) {
            tx.rollback();
        } finally {
            em.close();
        }
        emf.close();
    }

}
```

### SELECT

- find( ) 사용

```jsx
try {
    Member findMember = em.find(Member.class, 1L);
    System.out.println("findMember.id = " + findMember.getId());
    System.out.println("findMember.name = " + findMember.getName());

		tx.commit();
} catch (Exception e) {
```

- 결과

![Untitled](/images/jpa_crud/Untitled.png)

### UPDATE

- find( ) 사용
- setter 함수 사용

```jsx
try {
    Member findMember = em.find(Member.class, 1L);
    findMember.setName("HelloJPA");

    tx.commit();
} catch (Exception e) {
```

### DELETE

- find( ) 사용
- remove( ) 사용

```jsx
try {
    Member findMember = em.find(Member.class, 1L);
    em.removd(findMember);

		tx.commit();
} catch (Exception e) {
```

### SELECT 주의할 점

- 그냥 find( ) 사용으로는 불가능한 것도 있다
- 그럴 때 사용하는 것이 **JPQL**

## JPQL 개념

- 객체 대상으로 작동하는 쿼리
- 객체 지향 쿼리

![Untitled](/images/jpa_crud/Untitled%201.png)

![Untitled](/images/jpa_crud/Untitled%202.png)

---

## JPQL 사용법

![Untitled](/images/jpa_crud/Untitled%203.png)

### SELECT

- JPQL예시 코드

```jsx
try {
    List<Member> result = em.createQuery("select m from Member as m", Member.class)
            .getResultList();

    for (Member member : result) {
        System.out.println("Member.name = " + member.getName());
    }
```

- 결과

![Untitled](/images/jpa_crud/Untitled%204.png)