---
title: "Oracle_practice4"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-08'
---

# 조건식

### sql developer

- sql developer에서 새로운 sql 워크시트를 생성한다.
    
    도구 → sql워크시트 : 
    
- 오라클 SQL과 PL/SQL을 다루는 기술 92p

### 연산자

- 교재를 참고하여 코드를 익혀보자
- 연산자는 다음과 같이 사용한다.

```sql
-- 정리
-- 테이블 생성 : CREATE
-- 테이블 변경 (컬럼명, 데이터타입 등) : ALTER
-- 테이블 삭제 : DROP

-- 쿼리
-- SELECT (조회) FROM WHERE ORDER BY (...)
-- MERGE
-- 테이블 데이터 변경 : UPDATE SET
-- 테이블 특정 데이터 삭제 : DELETE

-- 연산자
DESC employees;

SELECT employee_id || '-' || emp_name AS employee_info
FROM employees;
```

![Untitled](/images/Oracle_practice_4/Untitled.png)

### 표현식

- 표현식이란 한 개 이상의 값과 연산자, SQL 함수 등이 결합된 식이다.
- 조건문은 다음과 같이 사용한다.
- CASE WHEN 조건 THEN ELSE END

```sql
-- 표현식 (조건문)
-- CASE WHEN 조건 THEN ELSE END
SELECT 
    employee_id
    , salary
    , CASE  WHEN salary <= 5000 THEN 'C등급'
            WHEN salary > 5000 AND salary <= 15000 THEN 'B등급'
            ELSE 'A등급'
      END AS salary_grade
FROM employees;
```

![Untitled](/images/Oracle_practice_4/Untitled%201.png)

### 조건식

- 조간 혹은 조건식은 한 개 이상의 표현식과 논리 연산자가 결합된 식으로 TRUE, FALSE, UNKNOWN 세 가지 타입을 반환한다.
- 지금까지 SQL문을 학습하면서 WHERE절에서 사용했던 모든 조건이 바로 조건식에 포함된다.

### 비교 조건식

- 비교 조건식 : ANY, SOME, ALL 키워드로 비교하는 조건식

### ANY

- ANY - OR 조건식을 사용해본다.

```sql
-- p.114
-- 비교 조건식 : ANY, SOME, ALL 키워드로 비교하는 조건식
-- ANY - OR
SELECT
    employee_id
    , salary
FROM employees
WHERE salary = 2000 or salary = 3000 or salary = 4000
```

- ANY가 ‘아무것’이나 ‘하나’라는 뜻이 있으므로 위 코드는 salary(급여)가 2000이나 3000이나 4000 중 하나라도 일치하는 모든 사원을 추출한 것이다.
- 하나라도 일치하면 추출하는 것이므로 ANY는 OR로 표현이 가능하다.

![Untitled](/images/Oracle_practice_4/Untitled%202.png)

### ALL

- ALL 조건문을 사용해본다.
- ALL이므로 모든 조건을 만족하는 것만 추출한다.
- ALL 조건식은 AND 조건으로 변환할 수 있다.

```sql
-- ALL
-- 모든 조건을 동시에 만족해야 함
SELECT
    employee_id
    , salary
FROM employees
WHERE salary = ALL(2000, 3000, 4000)
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%203.png)

### SOME

- SOME 조건문을 사용한다.
- SOME은 ANY와 동일하게 사용되며 동작한다.

```sql
-- SOME 
SELECT
    employee_id
    , salary
FROM employees
WHERE salary = SOME(2000, 3000, 4000)
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%204.png)

### 논리 조건식

- 논리 조건식 = 조건절에서 AND, OR, NOT을 사용하는 조건식
- AND는 모든 조건을 만족해야 하고 OR는 여러 조건 중 하나만 만족해도 TRUE를 반환된다.
- NOT은 조건식 평가 결과가 **거짓(FALSE)**일 때 원하는 결과, 즉 TRUE를 반환한다.

- NOT을 사용해본다.

```sql
-- 논리 조건식
SELECT 
    employee_id
    , salary
FROM employees
WHERE NOT (salary >= 2500)
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%205.png)

### BETWEEN AND 조건식

- BETWEEN은 범위에 해당되는 값을 찾을 때 사용하는데 크거나 같고 작거나 같은 값을 찾는다.
    - 따라서 ‘>=’와 ‘<=’ 논리 연산자로 변환이 가능하다.

```sql
-- BETWEEN AND 조건식
-- 범위 지정
-- 급여가 2000~2500 사이에 해당하는 사원을 조회하라
SELECT
    employee_id
    , salary
FROM employees
WHERE salary BETWEEN 2000 AND 2500
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%206.png)

### IN 조건식

- OR, ANY와 같은 기능을 수행 가능하다.
- IN 조건식은 조건절에 명시한 값이 포함된 건을 반환하는데 앞에서 배웠던 ANY와 비슷하다.

```sql
-- IN 조건식
-- OR - ANY 조건식과 비슷하다
SELECT
    employee_id
    , salary
FROM employees
WHERE salary IN (2000, 3000, 4000)
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%207.png)

### NOT IN 조건식

- IN 조건식과 반대의 결과를 출력한다.

```sql
-- NOT IN
SELECT
    employee_id
    , salary
FROM employees
WHERE salary NOT IN (2000, 3000, 4000)
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_4/Untitled%208.png)

### EXISTS 조건식

- XISTS 조건식 역시 IN과 비슷하지만 후행 조건절로 값의 리스트가 아닌 서브 쿼리만 올 수 있다.
- 또한 서브 쿼리 내에서 조인 조건(a.department_id = b.department_id)이 있어야 한다.

```sql
-- EXISTS 조건식
-- IN과 비슷함, 단 서브쿼리 절에만 사용 가능
SELECT department_id
       , department_name
FROM departments a
WHERE EXISTS (  SELECT *
                FROM employees b
                WHERE a.department_id = b.department_id
                AND b.salary > 3000)
ORDER BY a.department_name;
```

- 서브쿼리 부분이 메인이다.

![Untitled](/images/Oracle_practice_4/Untitled%209.png)

### LIKE 조건식

- LIKE 조건식은 문자열의 패턴을 검색할 때 사용하는 조건식이다.
- 예를 들어, 사원 테이블에서 사원이름이 ‘A’로 시작되는 사원을 조회하는 쿼리를 작성한다면 다음과 같이 LIKE 조건식을 사용.

```sql
-- LIKE 조건식
-- 문자열의 패턴을 검색할 때 사용하는 조건식
-- 사원 테이블 사원 이름이 'A'로 시작되는 사원 조회
SELECT emp_name
FROM employees
WHERE emp_name LIKE 'A%'
ORDER BY emp_name;
```

![Untitled](/images/Oracle_practice_4/Untitled%2010.png)

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술