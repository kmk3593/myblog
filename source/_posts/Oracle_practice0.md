---
title: "Oracle_practice0"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-16'
---

- p.205 6장 Self Check 6문제
- p.256~257 7징 Self Check 5문제


```python
%load_ext sql
```


```python
%sql oracle://ora_user:evan@127.0.0.1:1521/myoracle
```
1. 101번 사원에 대해 아래의 결과를 산출하는 쿼리를 작성해 보자.

    ---------------------------------------------------------------------------------------
    사번    사원명     job명칭     job시작일자     job종료일자        job수행부서명
    ----------------------------------------------------------------------------------

```sql
%%sql

SELECT 
    a.employee_id
    , a.emp_name
    , d.job_title
    , b.start_date
    , b.end_date
    , c.department_name
FROM employees a
    , job_history b 
    , departments c
    , jobs d
WHERE a.employee_id = b.employee_id
    AND b.department_id = c.department_id
    AND b.job_id        = d.job_id
    AND a.employee_id = 101
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>employee_id</th>
        <th>emp_name</th>
        <th>job_title</th>
        <th>start_date</th>
        <th>end_date</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>101</td>
        <td>Neena Kochhar</td>
        <td>Public Accountant</td>
        <td>1997-09-21 00:00:00</td>
        <td>2001-10-27 00:00:00</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>101</td>
        <td>Neena Kochhar</td>
        <td>Accounting Manager</td>
        <td>2001-10-28 00:00:00</td>
        <td>2005-03-15 00:00:00</td>
        <td>경리부</td>
    </tr>
</table>


2. 아래의 쿼리를 수행하면 오류가 발생한다. 오류의 원인은 무엇인지 설명해 보자.

입력

    select a.employee_id, a.emp_name, b.job_id, b.department_id
      from employees a,
           job_history b
     where a.employee_id      = b.employee_id(+)
       and a.department_id(+) = b.department_id;답 : 외부 조인의 경우, 조인조건에서 데이터가 없는 테이블의 컬럼에만 (+)를 붙여야 한다.
    따라서 위 쿼리의 경우, and a.department_id(+) 가 아닌 a.department_id = b.department_id(+)로 고쳐야 한다.3. 외부 조인을 할 때 (+)연산자를 같이 사용할 수 없는데, IN 절에 사용하는 값이 한 개이면 사용할 수 있다. 
그 이유는 무엇인지 설명해 보자.답 :
오라클은 IN 절에 포함된 값을 기준으로 OR로 변환한다.
예를 들어,
    department_id IN (10,20,30)은
    department_id = 10
    OR department_id = 20
    OR department_id = 30 으로 바꿔 쓸 수 있다.

그런데 IN절에 값이 1개인 경우, 즉 department_id IN (10)일 경우 department_id=10으로 변환할 수 있으며,
외부조인을 하더라도 값이 1개인 경우는 사용할 수 있다.4. 다음의 쿼리를 ANSI 문법으로 변경해 보자.

입력

    SELECT a.department_id, a.department_name
      FROM departments a, employees b
     WHERE a.department_id = b.department_id
       AND b.salary > 3000
    ORDER BY a.department_name;

```sql
%%sql

SELECT 
    a.department_id
    , a.department_name
FROM departments a
INNER JOIN employees b
    ON (a.department_id = b.department_id)
WHERE b.salary > 3000
ORDER BY a.department_name
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>110</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>110</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>30</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>30</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>20</td>
        <td>마케팅</td>
    </tr>
    <tr>
        <td>20</td>
        <td>마케팅</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>40</td>
        <td>인사부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>10</td>
        <td>총무기획부</td>
    </tr>
    <tr>
        <td>70</td>
        <td>홍보부</td>
    </tr>
</table>


5. 다음은 연관성 있는 서브 쿼리다. 이를 연관성 없는 서브 쿼리로 변환해 보자.

입력

    SELECT a.department_id, a.department_name
     FROM departments a
    WHERE EXISTS ( SELECT 1
                     FROM job_history b
                    WHERE a.department_id = b.department_id );

```sql
%%sql

SELECT 
    a.department_id, a.department_name
FROM departments a
WHERE a.department_id IN(SELECT department_id
                         FROM job_history)
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>20</td>
        <td>마케팅</td>
    </tr>
    <tr>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>110</td>
        <td>경리부</td>
    </tr>
</table>


6. 연도별 이탈리아 최대매출액과 사원을 작성하는 쿼리를 학습했다. 
이 쿼리를 기준으로 최대매출액 뿐만 아니라 최소매출액과 해당 사원을 조회하는 쿼리를 작성해 보자.

```sql
%%sql

SELECT 
    emp.years
    , emp.employee_id
    , emp2.emp_name
    , emp.amount_sold
FROM ( SELECT 
          SUBSTR(a.sales_month, 1, 4) as years
          , a.employee_id
          , SUM(a.amount_sold) AS amount_sold
        FROM
          sales a
          , customers b
          , countries c
        WHERE a.cust_id = b.CUST_ID
          AND b.country_id = c.COUNTRY_ID
          AND c.country_name = 'Italy'     
      GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id   
        ) emp,
       ( SELECT
            years
            , MAX(amount_sold) AS max_sold
            , MIN(amount_sold) AS min_sold
          FROM ( SELECT 
                    SUBSTR(a.sales_month, 1, 4) as years
                    , a.employee_id
                    , SUM(a.amount_sold) AS amount_sold
                   FROM 
                    sales a
                    , customers b
                    , countries c
                  WHERE a.cust_id = b.CUST_ID
                    AND b.country_id = c.COUNTRY_ID
                    AND c.country_name = 'Italy'     
                  GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id    
                    ) K
          GROUP BY years
       ) sale,
       employees emp2
WHERE emp.years = sale.years
    AND (emp.amount_sold = sale.max_sold  OR emp.amount_sold = sale.min_sold)
    AND emp.employee_id = emp2.employee_id
    ORDER BY years
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>years</th>
        <th>employee_id</th>
        <th>emp_name</th>
        <th>amount_sold</th>
    </tr>
    <tr>
        <td>1998</td>
        <td>145</td>
        <td>John Russell</td>
        <td>311761.02</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>145</td>
        <td>John Russell</td>
        <td>4646.74</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>147</td>
        <td>Alberto Errazuriz</td>
        <td>193319.44</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>153</td>
        <td>Christopher Olsen</td>
        <td>142987.82</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>162</td>
        <td>Clara Vishney</td>
        <td>16259.5</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>173</td>
        <td>Sundita Kumar</td>
        <td>426018.7</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>148</td>
        <td>Gerald Cambrault</td>
        <td>1557.54</td>
    </tr>
</table>


- 7장1. 계층형 쿼리 응용편에서 LISTAGG 함수를 사용해 다음과 같이 로우를 컬럼으로 분리했다.

입력

    SELECT department_id, LISTAGG(emp_name, ',') WITHIN GROUP (ORDER BY emp_name) as empnames
      FROM employees
     WHERE department_id IS NOT NULL
     GROUP BY department_id;
     
LISTAGG 함수 대신 계층형 쿼리, 분석 함수를 사용해서 위 쿼리와 동일한 결과를 산출하는 쿼리를 작성해 보자.2. 다음 쿼리는 사원 테이블에서 JOB_ID가 ‘SH_CLERK’인 사원을 조회하는 쿼리다.

입력

    SELECT employee_id, emp_name, hire_date
      FROM employees
     WHERE job_id = 'SH_CLERK'
    ORDER By hire_date;
    
 결과

    EMPLOYEE_ID EMP_NAME             HIRE_DATE
    ----------- -------------------- -------------------
    184         Nandita Sarchand     2004/01/27 00:00:00
    192         Sarah Bell           2004/02/04 00:00:00
    185         Alexis Bull          2005/02/20 00:00:00
    193         Britney Everett      2005/03/03 00:00:00
    188         Kelly Chung          2005/06/14 00:00:00
    ....
    ....
    199         Douglas Grant        2008/01/13 00:00:00
    183         Girard Geoni         2008/02/03 00:00:00
사원 테이블에서 퇴사일자(retire_date)는 모두 비어 있는데, 위 결과에서 사원번호가 184번인 사원의 퇴사일자는 다음으로 입사일자가 빠른 192번 사원의 입사일자라고 가정해서 다음과 같은 형태로 결과를 추출하도록 쿼리를 작성해 보자(입사일자가 가장 최근인 183번 사원의 퇴사일자는 NULL이다).

결과

    EMPLOYEE_ID EMP_NAME             HIRE_DATE            RETIRE_DATE
    ----------- -------------------- -------------------  ---------------------------
    184         Nandita Sarchand     2004/01/27 00:00:00  2004/02/04 00:00:00
    192         Sarah Bell           2004/02/04 00:00:00  2005/02/20 00:00:00
    185         Alexis Bull          2005/02/20 00:00:00  2005/03/03 00:00:00
    193         Britney Everett      2005/03/03 00:00:00  2005/06/14 00:00:00
    188         Kelly Chung          2005/06/14 00:00:00  2005/08/13 00:00:00
    ....
    ....
    199         Douglas Grant        2008/01/13 00:00:00  2008/02/03 00:00:00
    183         Girard Geoni         2008/02/03 00:00:003. sales 테이블에는 판매 데이터, customers 테이블에는 고객정보가 있다. 2001년 12월(SALES_MONTH = ‘200112’) 판매 데이터 중 현재일자를 기준으로 고객의 나이(customers.cust_year_of_birth)를 계산해서 다음과 같이 연령대별 매출금액을 보여주는 쿼리를 작성해 보자.

결과

    -------------------------
    연령대    매출금액
    -------------------------
    10대      xxxxxx
    20대      ....
    30대      ....
    40대      ....
    -------------------------4. 3번 문제를 이용해 월별로 판매금액이 가장 하위에 속하는 대륙 목록을 뽑아보자.
(대륙 목록은 countries 테이블의 country_region에 있으며, country_id 컬럼으로 customers 테이블과 조인을 해서 구한다).

결과

    ---------------------------------
    매출월    지역(대륙)  매출금액
    ---------------------------------
    199801    Oceania      xxxxxx
    199803    Oceania      xxxxxx
    ...
    ---------------------------------5. 5장 연습문제 5번의 정답 결과를 이용해 다음과 같이 지역별, 대출종류별, 월별 대출잔액과 지역별 파티션을 만들어 대출 종류별 대출잔액의 퍼센트(%)를 구하는 쿼리를 작성해보자.

결과

    ------------------------------------------------------------------------------------------------
    지역    대출종류        201111         201112    201210    201211   201212   203110    201311
    ------------------------------------------------------------------------------------------------
    서울    기타대출       73996.9( 36% )
    서울    주택담보대출   130105.9( 64% )
    부산
    ...
    ...
    --------------------------------------------------------------------------------------