---
title: "JPA 영속석 컨텍스트"
tags:
  - JPA
  - JPA 기초
categories:
  - JPA
author: "minkuen"
date: '2023-06-15'
---

# 엔티티 매핑

[강의] ****자바 ORM 표준 JPA 프로그래밍 - 기본편****

---

### Mapping 소개

- 객체와 테이블  : @Entity, @Table
- 필드와 컬럼 : @Column
- 기본 키 : @Id
- 연관 관계 : @ManyToOne,@JoinColumn

### @Entity

- @Entity가 붙은 클래스는 **JPA가 관리**, 엔티티라 한다.
- JPA를 사용해서 **테이블과 매핑할 클래스**는 @Entity 필수
- 주의
    - 기본 생성자 필수(파라미터가 없는 public 또는 protected 생성자)
    - final 클래스, enum, interface, inner 클래스 사용X
    - 저장할 필드에 final 사용 X

### @Table

- @Table은 Entity와 매핑할 테이블 지정

![Untitled](/images/jpa_mapping/Untitled.png)

### 데이터베이스 스키마 자동 생성

- DDL을 애플리케이션 **실행 시점에 자동 생성**
- 테이블 중심 -> 객체 중심
- 데이터베이스 방언을 활용해서 데이터베이스에 맞는 **적절한 DDL 생성**
- 이렇게 생성된 DDL은 **개발 장비에서만 사용**
- 생성된 DDL은 운영서버에서는 사용하지 않거나, 적절히 다듬은 후 사용

### 데이터베이스 스키마 자동 생성 - 속성

- hibernate.hbm2ddl.auto
- persistence.xml 에서 사용 가능하다

```jsx
<properties>

    <!-- 필수 속성 -->
		<!-- 드라이버, id, password, localhost 등 -->
		...
		...

    <!-- 옵션 -->
    <!-- 실행 시, 쿼리 문을 보여주는 옵션, 줄 맞춰주는 옵션 등 -->
		...
		...
    <property name="**hibernate.hbm2ddl.auto**" value="**옵션**" />

</properties>
```

- 옵션

![Untitled](/images/jpa_mapping/Untitled%201.png)

### DB 스키마 자동 생성 - 실습

- persistence.xml 에서 원하는 옵션으로 적어넣는다.
- **@Entity 사용된 파일**에서 옵션을 고려하여 변경하거나 그대로 둔다
- 하던 것처럼 Run 하여 실행시킨다
- H2 DB 확인하면 반영된 것을 확인 가능

### 데이터베이스 스키마 자동 생성 - 주의점

- **운영 장비에는 절대 create, create-drop, update 사용하면 안된다.**
- 개발 진행 중에만 사용해야 한다

- 개발 초기 단계는 create 또는 update
- 테스트 서버는 update 또는 validate
- 스테이징과 운영 서버는 validate 또는 none

---

# 필드와 컬럼 매핑

- 실습 상황
1. 회원은 일반 회원과 관리자로 구분해야 한다.
2. 회원 가입일과 수정일이 있어야 한다.
3. 회원을 설명할 수 있는 필드가 있어야 한다. 이 필드는 길이 제
한이 없다.

```jsx
package hellojpa; 
import javax.persistence.*; 
import java.time.LocalDate; 
import java.time.LocalDateTime; 
import java.util.Date; 
@Entity 
public class Member { 
		 @Id 
		 private Long id; 

		 @Column(name = "name") 
		 private String username; 

		 private Integer age; 

		 @Enumerated(EnumType.STRING) 
		 private RoleType roleType; 

		 @Temporal(TemporalType.TIMESTAMP) 
		 private Date createdDate; 

		 @Temporal(TemporalType.TIMESTAMP) 
		 private Date lastModifiedDate; 

		 @Lob 
		 private String description; 

 //Getter, Setter… 
}
```

### 매핑 어노테이션 정리

- hibernate.hbm2ddl.auto

![Untitled](/images/jpa_mapping/Untitled%202.png)

### @COLUMN

![Untitled](/images/jpa_mapping/Untitled%203.png)

- column 어노테이션 - 사용 예시

```jsx
@column ( name = “테이블 컬럼 이름”, nullable = false )
private String username; 
```

### @Enumerated

- 자바 enum 타입을 매핑할 때 사용
- 주의! ORDINAL 사용X

![Untitled](/images/jpa_mapping/Untitled%204.png)

- ORDINAL = 순서 저장 ( DEFAULT 설정 )
    - 숫자로 저장된다 ( Integer )
- **STRING = 이름 저장 ( 이것만 사용하자 )**

- **주의! ORDINAL 사용X**
    - 순서를 저장하지만 순서가 꼬일 수 있다

### Enum 개념

- Enum = **관련 있는 상수들의 집합**
- 상수 = final, String 등으로 고정된 값 (영어로는 Constant)
- 예시

```jsx
// RoleType.java
public enum RoleType {
    USER, ADMIN
}
```

- 사용예시
    - @Entity 페이지에서 선언하고
    - enum 클래스에 있는 값 중에서 넣어서 사용한다

```jsx
//Member.java
@Enumerated(EnumType.**STRING**)
private RoleType roleType;

// JpaMain.java
Member member = new Member();
member.setRoleType(RoleType.User);
```

### @Temporal

- 날짜 타입(java.util.**Date**,   java.util.**Calendar**)을 매핑할 때 사용
- 참고: Local**Date**, Local**DateTime**을 사용할 때는 생략 가능(최신 하이버네이트 지원)

![Untitled](/images/jpa_mapping/Untitled%205.png)

### @LOB

- 데이터베이스 BLOB, CLOB 타입과 매핑
- @Lob에는 지정할 수 있는 속성이 없다.
- 매핑하는 필드 타입이 **문자면 CLOB** 매핑, **나머지는 BLOB** 매핑

- **CLOB: String,   char[],   java.sql.CLOB**
- **BLOB: byte[],   java.sql. BLOB**

### @Transient

- 필드 매핑X
- 데이터베이스에 저장X, 조회X
- 주로 **메모리 상에서만 임시로 어떤 값을 보관**하고 싶을 때 사용
- 예시

```jsx
@Transient
private Integer temp;
```

---

## 기본키 매핑

### 기본 키 매핑 어노테이션

- **@Id**
- **@GeneratedValue**

```jsx
@Id 
@GeneratedValue(strategy = GenerationType.**옵션**)
private Long id;
```

- 직접 할당: @Id만 사용

- **자동 생성**(@GeneratedValue) **옵션**

![Untitled](/images/jpa_mapping/Untitled%206.png)

- 사용자가 지정해주지 않아도 알아서 값이 들어간다
    - 1부터 들어간다

### IDENTITY 전략 - 특징

- **기본 키 생성**을 **DB에 위임**
- 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용
(**예시**: MySQL의 **AUTO_ INCREMENT**)
- JPA는 보통 트랜잭션 커밋 시점에 INSERT SQL 실행
- **AUTO_ INCREMENT**는 데이터베이스에 INSERT SQL을 실행한 이후에 ID 값을 알 수 있음
- IDENTITY 전략은 em.persist() 시점에 즉시 INSERT SQL 실행하고 DB에서 식별자를 조회
- 코드

```jsx
@Entity 
public class Member { 

			 @Id 
			 @GeneratedValue(strategy = GenerationType.**IDENTITY**) 
			 private Long id;
```

### SEQUENCE 전략 - 특징

- DB 시퀀스는 유일한 값을 순서대로 생성하는 특별한 DB 오브젝트 (**예시:** 오라클 **시퀀스**)
- 오라클, PostgreSQL, DB2, H2 데이터베이스에서 사용
- 코드

```jsx
@Entity 
@SequenceGenerator( 
		 name = "MEMBER_SEQ_GENERATOR", 
		 sequenceName = "MEMBER_SEQ",
		 initialValue = 1, allocationSize = 1)
public class Member { 
		 @Id 
		 @GeneratedValue(strategy = GenerationType.**SEQUENCE**, 
		 generator = "MEMBER_SEQ_GENERATOR") 
		 private Long id;
```

### SEQUENCE - @SequenceGenerator

- 주의: allocationSize 기본값 = 50

![Untitled](/images/jpa_mapping/Untitled%207.png)

### Table 전략

- 키 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내내는 전략
    - 장점: 모든 데이터베이스에 적용 가능
    - 단점: 성능
- 코드

```jsx
create table MY_SEQUENCES ( 
		 sequence_name varchar(255) not null, 
		 next_val bigint, 
		 primary key ( sequence_name ) 
)
```

```jsx
Entity 
@TableGenerator( 
		 name = "MEMBER_SEQ_GENERATOR", 
		 table = "MY_SEQUENCES", 
		 pkColumnValue = “MEMBER_SEQ", allocationSize = 1) 
public class Member { 
		 @Id 
		 @GeneratedValue(strategy = GenerationType.TABLE, 
		 generator = "MEMBER_SEQ_GENERATOR") 
		 private Long id;
```

### @TableGenerator - 속성

- 잘 안 쓰임

![Untitled](/images/jpa_mapping/Untitled%208.png)

### 권장하는 식별자 전략

- 기본 키 제약 조건
    - not Null
    - 유일
    - 변하면 안된다.
- 미래까지 이 조건을 만족하는 자연키는 찾기 어렵다. 대리키(대체키)를 사용하자.
    - 예를 들어 주민등록번호도 기본 키로 적절하기 않다.
- **권장**
    - **Long형 + 대체키 + 키 생성전략 사용**

### 실습

- 회원은 상품을 주문할 수 있다.
- 주문 시 여러 종류의 상품을 선택할 수 있다

- 회원과 주문의 관계: 회원은 여러 번 주문할 수 있다. (일대다)
- 주문과 상품의 관계: 주문할 때 여러 상품을 선택할 수 있다. 반
대로 같은 상품도 여러 번 주문될 수 있다.
- 주문상품 이라는 모델을 만들어서 다대다 관계를 일다대, 다대일 관계로 풀어냄

![Untitled](/images/jpa_mapping/Untitled%209.png)

- ERD

![Untitled](/images/jpa_mapping/Untitled%2010.png)

D:\study\jpashop\src\main\java\jpabook\resources\META_INF