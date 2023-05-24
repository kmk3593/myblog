---
title: "JPA 개념"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-05-24'
---

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****
---


# JPA 개념


**ORM(Object-Relational Mapping)**

- **우리가 일반 적으로 알고 있는 애플리케이션 Class와 RDB(Relational DataBase)의 테이블을 매핑(연결)한다는 뜻이며, 기술적으로는 어플리케이션의 객체를 RDB 테이블에 자동으로 영속화 해주는 것이라고 보면된다.**

![Untitled](/images/jpa_base/Untitled.png)

**JPA(Java Persistence API)**

- Java 진영에서 ORM(Object-Relational Mapping) 기술 표준으로 사용하는 인터페이스 모음
- 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스
- 인터페이스 이기 때문에 Hibernate, OpenJPA 등이 JPA를 구현함

- data 가져다 DB에 넣는 것처럼, 객체를 DB에 넣을 수 있지 않을까? ⇒ JPA

![Untitled](/images/jpa_base/Untitled%201.png)

![Untitled](/images/jpa_base/Untitled%202.png)

![Untitled](/images/jpa_base/Untitled%203.png)

![Untitled](/images/jpa_base/Untitled%204.png)

---

## 생산성 - JPA와 CRUD

- 저장 : `JPA.persist (member)`
- 조회 : `Member member = jpa.find (member Id)`
- 수정 : `member.setName (”변경할 이름”)`
- 삭제 : `jpa.remove (member)`

![Untitled](/images/jpa_base/Untitled%205.png)

![Untitled](/images/jpa_base/Untitled%206.png)

![Untitled](/images/jpa_base/Untitled%207.png)

- 어떤 것을 설명하는지 잘??

---

![Untitled](/images/jpa_base/Untitled%208.png)

![Untitled](/images/jpa_base/Untitled%209.png)

---

### JPA 성능 최적화 기능

- 1차 캐시와 동일성 (identify) 보장
- 트랜잭션을 지원하는 쓰기 지연 (transactional write-behind)
- 지연 로딩(Lazy Loading)

![Untitled](/images/jpa_base/Untitled%2010.png)

![Untitled](/images/jpa_base/Untitled%2011.png)

![Untitled](/images/jpa_base/Untitled%2012.png)

![Untitled](/images/jpa_base/Untitled%2013.png)