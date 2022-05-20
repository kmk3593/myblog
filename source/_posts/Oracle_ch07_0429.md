---
title: "Oracle_practice7_2"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-15'
---

- 분석함수 : RANK, DENSE_RANK, LAG, LEAD
- RANK() OVER (PARTITION BY 컬럼명 ORDER BY 컬럼명)


```python
%load_ext sql
```

    The sql extension is already loaded. To reload it, use:
      %reload_ext sql
    


```python
%sql oracle://ora_user:evan@127.0.0.1:1521/myoracle
```
- 분석 함수: 분석 함수 역시 특정 그룹별 집계를 담당하므로 집계 함수에 속한다. 
- PARTITION BY 절: 분석 함수로 계산될 대상 로우의 그룹(파티션)을 지정한다.
- ORDER BY 절: 파티션 안에서의 순서를 지정한다.
- WINDOW 절: 파티션으로 분할된 그룹에 대해서 더 상세한 그룹으로 분할할 때 사용된다. # Window 절 

- ROWS: 로우 단위로 window 절을 지정한다.
- RANGE: 로우가 아닌 논리적인 범위로 window 절을 지정한다.
- BETWEEN~AND: window 절의 시작과 끝 지점을 명시한다. 
               BETWEEN을 명시하지 않고 두 번째 옵션만 지정하면이 지점이 시작 지점이 되고 끝 지점은 현재 로우가 된다.
    
- UNBOUNDED PRECEDING: 파티션으로 구분된 첫 번째 로우가 시작 지점이 된다.
- UNBOUNDED FOLLOWING: 파티션으로 구분된 마지막 로우가 끝 지점이 된다.

- CURRENT ROW: 시작 및 끝 지점이 현재 로우가된다.
- value_expr PRECEDING: 끝 지점일 경우, 시작 지점은 value_expr PRECEDING.
- value_expr FOLLOWING: 시작 지점일 경우, 끝 지점은 value_expr FOLLOWING.

```sql
%%sql

SELECT
    department_id
    , emp_name
    , hire_date
    , salary
    , SUM(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS all_salary
    , SUM(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS first_current_sal
    , SUM(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                        ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS current_end_sal
FROM employees
WHERE department_id IN (30, 90)
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>hire_date</th>
        <th>salary</th>
        <th>all_salary</th>
        <th>first_current_sal</th>
        <th>current_end_sal</th>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>2002-12-07 00:00:00</td>
        <td>11000</td>
        <td>24900</td>
        <td>11000</td>
        <td>24900</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>2003-05-18 00:00:00</td>
        <td>3100</td>
        <td>24900</td>
        <td>14100</td>
        <td>13900</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>2005-07-24 00:00:00</td>
        <td>2800</td>
        <td>24900</td>
        <td>16900</td>
        <td>10800</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>2005-12-24 00:00:00</td>
        <td>2900</td>
        <td>24900</td>
        <td>19800</td>
        <td>8000</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>2006-11-15 00:00:00</td>
        <td>2600</td>
        <td>24900</td>
        <td>22400</td>
        <td>5100</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>2007-08-10 00:00:00</td>
        <td>2500</td>
        <td>24900</td>
        <td>24900</td>
        <td>2500</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Lex De Haan</td>
        <td>2001-01-13 00:00:00</td>
        <td>17000</td>
        <td>58000</td>
        <td>17000</td>
        <td>58000</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Steven King</td>
        <td>2003-06-17 00:00:00</td>
        <td>24000</td>
        <td>58000</td>
        <td>41000</td>
        <td>41000</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Neena Kochhar</td>
        <td>2005-09-21 00:00:00</td>
        <td>17000</td>
        <td>58000</td>
        <td>58000</td>
        <td>17000</td>
    </tr>
</table>




```sql
%%sql

SELECT
    department_id
    , emp_name
    , hire_date
    , salary
    , FIRST_VALUE(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS all_salary
    , FIRST_VALUE(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS first_current_sal
    , FIRST_VALUE(salary) OVER (PARTITION BY department_id
                        ORDER BY hire_date
                        ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS current_end_sal
FROM employees
WHERE department_id IN (30, 90)
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>hire_date</th>
        <th>salary</th>
        <th>all_salary</th>
        <th>first_current_sal</th>
        <th>current_end_sal</th>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>2002-12-07 00:00:00</td>
        <td>11000</td>
        <td>11000</td>
        <td>11000</td>
        <td>11000</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>2003-05-18 00:00:00</td>
        <td>3100</td>
        <td>11000</td>
        <td>11000</td>
        <td>3100</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>2005-07-24 00:00:00</td>
        <td>2800</td>
        <td>11000</td>
        <td>11000</td>
        <td>2800</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>2005-12-24 00:00:00</td>
        <td>2900</td>
        <td>11000</td>
        <td>11000</td>
        <td>2900</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>2006-11-15 00:00:00</td>
        <td>2600</td>
        <td>11000</td>
        <td>11000</td>
        <td>2600</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>2007-08-10 00:00:00</td>
        <td>2500</td>
        <td>11000</td>
        <td>11000</td>
        <td>2500</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Lex De Haan</td>
        <td>2001-01-13 00:00:00</td>
        <td>17000</td>
        <td>17000</td>
        <td>17000</td>
        <td>17000</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Steven King</td>
        <td>2003-06-17 00:00:00</td>
        <td>24000</td>
        <td>17000</td>
        <td>17000</td>
        <td>24000</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Neena Kochhar</td>
        <td>2005-09-21 00:00:00</td>
        <td>17000</td>
        <td>17000</td>
        <td>17000</td>
        <td>17000</td>
    </tr>
</table>


- p.211
- 계층형 쿼리
- 핵심 포인트 : CONNECT BY 조건문 정리- 계층형 쿼리의 구문은 다음과 같다.

SELECT expr1, expr2, ...
FROM 테이블
WHERE 조건
START WITH[최상위 조건]
CONNECT BY [NOCYCLE][PRIOR 계층형 구조 조건];       --> 구조 :  CONNECT BY PRIOR 하위 = 상위 

- START WITH 조건
    - 계층형 구조에서 최상위 계층의 로우를 식별하는 조건을 명시한다. 
    - START WITH가 시작한다는 의미이므로, 이 조건에 맞는 로우부터 시작해 계층형 구조를 풀어 나간다.

- CONNECT BY 조건
    - 계층형 구조가 어떤 식으로 연결되는지를 기술하는 부분이다.
    - 부서 테이블은 parent_id에 상위 부서 정보를 갖고 있는데, 
    이를 표현하려면 ‘CONNECT BY PRIOR department_id = parent_id’로 기술해야 한다. 
    - PRIOR는 계층형 쿼리에서만 사용할 수 있는 연산자로 ‘앞서의, 직전의’란 뜻이 있으므로, 
    “이전 department_id = parent_id”라고 알아두면 이해하기 쉬울 것이다. 
    - 또한 ‘CONNECT BY parent_id = PRIOR department_id’처럼 PRIOR의 위치를 바꿀 수 있다.

```sql
%%sql

SELECT
    department_id
    , LPAD(' ', 3*(LEVEL-1)) || department_name
    , LEVEL
FROM departments
START WITH parent_id IS NULL
CONNECT BY PRIOR department_id = parent_id 
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>LPAD(&#x27;&#x27;,3*(LEVEL-1))||DEPARTMENT_NAME</th>
        <th>LEVEL</th>
    </tr>
    <tr>
        <td>10</td>
        <td>총무기획부</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>&nbsp;&nbsp;&nbsp;마케팅</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>&nbsp;&nbsp;&nbsp;구매/생산부</td>
        <td>2</td>
    </tr>
    <tr>
        <td>170</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;생산팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>180</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;건설팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>200</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;운영팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>210</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IT 지원</td>
        <td>3</td>
    </tr>
    <tr>
        <td>220</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NOC</td>
        <td>3</td>
    </tr>
    <tr>
        <td>40</td>
        <td>&nbsp;&nbsp;&nbsp;인사부</td>
        <td>2</td>
    </tr>
    <tr>
        <td>260</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;채용팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>50</td>
        <td>&nbsp;&nbsp;&nbsp;배송부</td>
        <td>2</td>
    </tr>
    <tr>
        <td>80</td>
        <td>&nbsp;&nbsp;&nbsp;영업부</td>
        <td>2</td>
    </tr>
    <tr>
        <td>190</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;계약팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>240</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;공공 판매사업팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>250</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;판매팀</td>
        <td>3</td>
    </tr>
    <tr>
        <td>90</td>
        <td>&nbsp;&nbsp;&nbsp;기획부</td>
        <td>2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IT</td>
        <td>3</td>
    </tr>
    <tr>
        <td>230</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IT 헬프데스크</td>
        <td>4</td>
    </tr>
    <tr>
        <td>70</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;홍보부</td>
        <td>3</td>
    </tr>
    <tr>
        <td>100</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;자금부</td>
        <td>3</td>
    </tr>
    <tr>
        <td>130</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;세무팀</td>
        <td>4</td>
    </tr>
    <tr>
        <td>140</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;신용관리팀</td>
        <td>4</td>
    </tr>
    <tr>
        <td>150</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;주식관리팀</td>
        <td>4</td>
    </tr>
    <tr>
        <td>160</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;수익관리팀</td>
        <td>4</td>
    </tr>
    <tr>
        <td>110</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;경리부</td>
        <td>3</td>
    </tr>
    <tr>
        <td>120</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;재무팀</td>
        <td>4</td>
    </tr>
    <tr>
        <td>270</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;급여팀</td>
        <td>4</td>
    </tr>
</table>


- manager_id는 해당 사원의 매니저 사번이 있다.
- 각 매니저는 사원 ID가 있다.
- 사원별 계층 구조를 만들고, 부서 테이블과 조인해서 부서명까지 조회한다.

```sql
%%sql

SELECT 
    a.employee_id
    , LPAD(' ', 3 * (LEVEL - 1)) || a.emp_name
    , LEVEL
    , b.department_name
FROM
    employees a
    , departments b
WHERE a.department_id = b.department_id
START WITH a.manager_id IS NULL
CONNECT BY PRIOR a.employee_id = a.manager_id
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>employee_id</th>
        <th>LPAD(&#x27;&#x27;,3*(LEVEL-1))||A.EMP_NAME</th>
        <th>LEVEL</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>100</td>
        <td>Steven King</td>
        <td>1</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>101</td>
        <td>&nbsp;&nbsp;&nbsp;Neena Kochhar</td>
        <td>2</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>108</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nancy Greenberg</td>
        <td>3</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>109</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Daniel Faviet</td>
        <td>4</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>110</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;John Chen</td>
        <td>4</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>111</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ismael Sciarra</td>
        <td>4</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>112</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jose Manuel Urman</td>
        <td>4</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>113</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Luis Popp</td>
        <td>4</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>200</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jennifer Whalen</td>
        <td>3</td>
        <td>총무기획부</td>
    </tr>
    <tr>
        <td>203</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Susan Mavris</td>
        <td>3</td>
        <td>인사부</td>
    </tr>
    <tr>
        <td>204</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hermann Baer</td>
        <td>3</td>
        <td>홍보부</td>
    </tr>
    <tr>
        <td>205</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shelley Higgins</td>
        <td>3</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>206</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;William Gietz</td>
        <td>4</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>102</td>
        <td>&nbsp;&nbsp;&nbsp;Lex De Haan</td>
        <td>2</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>103</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alexander Hunold</td>
        <td>3</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>104</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bruce Ernst</td>
        <td>4</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>105</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;David Austin</td>
        <td>4</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>106</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Valli Pataballa</td>
        <td>4</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>107</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Diana Lorentz</td>
        <td>4</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>114</td>
        <td>&nbsp;&nbsp;&nbsp;Den Raphaely</td>
        <td>2</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>115</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alexander Khoo</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>116</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shelli Baida</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>117</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sigal Tobias</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>118</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Guy Himuro</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>119</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Karen Colmenares</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>120</td>
        <td>&nbsp;&nbsp;&nbsp;Matthew Weiss</td>
        <td>2</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>125</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Julia Nayer</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>126</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Irene Mikkilineni</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>127</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;James Landry</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>128</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Steven Markle</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>180</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Winston Taylor</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>181</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jean Fleaur</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>182</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Martha Sullivan</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>183</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Girard Geoni</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>121</td>
        <td>&nbsp;&nbsp;&nbsp;Adam Fripp</td>
        <td>2</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>129</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Laura Bissot</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>130</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mozhe Atkinson</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>131</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;James Marlow</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>132</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TJ Olson</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>184</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nandita Sarchand</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>185</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alexis Bull</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>186</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Julia Dellinger</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>187</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Anthony Cabrio</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>122</td>
        <td>&nbsp;&nbsp;&nbsp;Payam Kaufling</td>
        <td>2</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>133</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jason Mallin</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>134</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Michael Rogers</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>135</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ki Gee</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>136</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Hazel Philtanker</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>188</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kelly Chung</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>189</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jennifer Dilly</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>190</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Timothy Gates</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>191</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Randall Perkins</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>123</td>
        <td>&nbsp;&nbsp;&nbsp;Shanta Vollman</td>
        <td>2</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>137</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Renske Ladwig</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>138</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Stephen Stiles</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>139</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;John Seo</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>140</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Joshua Patel</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>192</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sarah Bell</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>193</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Britney Everett</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>194</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Samuel McCain</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>195</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Vance Jones</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>124</td>
        <td>&nbsp;&nbsp;&nbsp;Kevin Mourgos</td>
        <td>2</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>141</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Trenna Rajs</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>142</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Curtis Davies</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>143</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Randall Matos</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>144</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peter Vargas</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>196</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alana Walsh</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>197</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Kevin Feeney</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>198</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Donald OConnell</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>199</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Douglas Grant</td>
        <td>3</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>145</td>
        <td>&nbsp;&nbsp;&nbsp;John Russell</td>
        <td>2</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>150</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peter Tucker</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>151</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;David Bernstein</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>152</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Peter Hall</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>153</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Christopher Olsen</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>154</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Nanette Cambrault</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>155</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Oliver Tuvault</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>146</td>
        <td>&nbsp;&nbsp;&nbsp;Karen Partners</td>
        <td>2</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>156</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Janette King</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>157</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Patrick Sully</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>158</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Allan McEwen</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>159</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lindsey Smith</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>160</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Louise Doran</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>161</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sarath Sewall</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>147</td>
        <td>&nbsp;&nbsp;&nbsp;Alberto Errazuriz</td>
        <td>2</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>162</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Clara Vishney</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>163</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Danielle Greene</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>164</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mattea Marvins</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>165</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;David Lee</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>166</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sundar Ande</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>167</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Amit Banda</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>148</td>
        <td>&nbsp;&nbsp;&nbsp;Gerald Cambrault</td>
        <td>2</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>168</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Lisa Ozer</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>169</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Harrison Bloom</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>170</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tayler Fox</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>171</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;William Smith</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>172</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Elizabeth Bates</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>173</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sundita Kumar</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>149</td>
        <td>&nbsp;&nbsp;&nbsp;Eleni Zlotkey</td>
        <td>2</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>174</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ellen Abel</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>175</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alyssa Hutton</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>176</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jonathon Taylor</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>177</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Jack Livingston</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>179</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Charles Johnson</td>
        <td>3</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>201</td>
        <td>&nbsp;&nbsp;&nbsp;Michael Hartstein</td>
        <td>2</td>
        <td>마케팅</td>
    </tr>
    <tr>
        <td>202</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Pat Fay</td>
        <td>3</td>
        <td>마케팅</td>
    </tr>
</table>


- CONNECT BY ~ AND : AND를 통해 추가로 조건을 붙인다.

```sql
%%sql

SELECT 
    a.employee_id
    , LPAD(' ', 3 * (LEVEL - 1)) || a.emp_name
    , LEVEL
    , b.department_name
FROM
    employees a
    , departments b
WHERE a.department_id = b.department_id
START WITH a.manager_id IS NULL
CONNECT BY PRIOR a.employee_id = a.manager_id
    AND a.department_id = 30
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>employee_id</th>
        <th>LPAD(&#x27;&#x27;,3*(LEVEL-1))||A.EMP_NAME</th>
        <th>LEVEL</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>100</td>
        <td>Steven King</td>
        <td>1</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>114</td>
        <td>&nbsp;&nbsp;&nbsp;Den Raphaely</td>
        <td>2</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>115</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Alexander Khoo</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>116</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Shelli Baida</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>117</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Sigal Tobias</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>118</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Guy Himuro</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>119</td>
        <td>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Karen Colmenares</td>
        <td>3</td>
        <td>구매/생산부</td>
    </tr>
</table>


- CONNECT BY PRIOR 자식컬럼 = 부모컬럼 : 부모에서 자식으로 트리 구성 (TOP DOWN) -> 일반적인 구조
- CONNECT BY PRIOR 부모컬럼 = 자식컬럼 : 자식에서 부모로 트리 구성 (Bottom UP)
- CONNECT BY NOCYCLE PRIOR = 무한루프 방지- p.226 WITH 절
- kor_loan_status 테이블에서 연도별 최종월 기준 가장 대출이 많은 도시와 잔액을 구한다.

```sql
%%sql

SELECT b2.*
FROM ( SELECT period, region, sum(loan_jan_amt) jan_amt
         FROM kor_loan_status 
         GROUP BY period, region
      ) b2,      
      ( SELECT b.period,  MAX(b.jan_amt) max_jan_amt
         FROM ( SELECT period, region, sum(loan_jan_amt) jan_amt
                  FROM kor_loan_status 
                 GROUP BY period, region
              ) b,
              ( SELECT MAX(PERIOD) max_month
                  FROM kor_loan_status
                 GROUP BY SUBSTR(PERIOD, 1, 4)
              ) a
         WHERE b.period = a.max_month
         GROUP BY b.period
      ) c   
 WHERE b2.period = c.period
   AND b2.jan_amt = c.max_jan_amt
 ORDER BY 1
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>period</th>
        <th>region</th>
        <th>jan_amt</th>
    </tr>
    <tr>
        <td>201112</td>
        <td>서울</td>
        <td>334728.3</td>
    </tr>
    <tr>
        <td>201212</td>
        <td>서울</td>
        <td>331572.3</td>
    </tr>
    <tr>
        <td>201311</td>
        <td>서울</td>
        <td>334062.7</td>
    </tr>
</table>




```python
- WITH 절은 별칭으로 사용한 SELECT 문의 FROM 절에 다른 SELECT 구문의 별칭 참조가 가능하다.
```

- WITH 동일 구문 반복 사용 시

```sql
%%sql

WITH b2 AS (SELECT period, region, sum(loan_jan_amt) jan_amt
         FROM kor_loan_status 
         GROUP BY period, region)
     , c AS (SELECT b.period, MAX(b.jan_amt) max_jan_amt
             FROM (SELECT period, region, sum(loan_jan_amt) jan_amt
                 FROM kor_loan_status 
                 GROUP BY period, region) b
                 , (SELECT MAX(PERIOD) max_month
                    FROM kor_loan_status
                    GROUP BY SUBSTR(PERIOD, 1, 4)
                 ) a
             WHERE b.period = a.max_month
             GROUP BY b.period
           ) -- AS SELECT 
SELECT b2.*
FROM b2, c
WHERE b2.period = c.period
    AND b2.jan_amt = c.max_jan_amt
ORDER BY 1
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>period</th>
        <th>region</th>
        <th>jan_amt</th>
    </tr>
    <tr>
        <td>201112</td>
        <td>서울</td>
        <td>334728.3</td>
    </tr>
    <tr>
        <td>201212</td>
        <td>서울</td>
        <td>331572.3</td>
    </tr>
    <tr>
        <td>201311</td>
        <td>서울</td>
        <td>334062.7</td>
    </tr>
</table>


- Reference : 오라클 SQL과 PL/SQK을 다루는 기술