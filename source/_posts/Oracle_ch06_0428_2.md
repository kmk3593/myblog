---
title: "Oracle_practice6_3"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-13'
---

- 6장 조인과 서브쿼리/후반

```python
%load_ext sql
```


```python
%sql oracle://ora_user:evan@127.0.0.1:1521/myoracle
```
- p.198
- 기획부 산하에 있는 부서에 속한 사원의 평균급여보다 많은 급여를 받는 사원- 서브쿼리
- 오전 : WHERE, SELECT
- 오후 : FROM
- 기획부 : 부서 테이블
- 급여 : 사원 테이블

SELECT 
    a.employee_id
    , a.emp_name
    , b.department_id
    , b.department_name
FROM
    employees a
    , departments b
    (서브쿼리) d -- 기획부 평균급여
WHERE a.deartment_id = b.department_id
    AND a.salary > d.avg_salary

```sql
%%sql

SELECT 
    a.employee_id
    , a.emp_name
    , b.department_id
    , b.department_name
FROM
    employees a
    , departments b
    , (SELECT AVG(c.salary) AS avg_salary
       FROM
       departments b
       , employees c
       WHERE b.parent_id = 90
       AND b.department_id = c.department_id) d
WHERE a.department_id = b.department_id
    AND a.salary > d.avg_salary
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>employee_id</th>
        <th>emp_name</th>
        <th>department_id</th>
        <th>department_name</th>
    </tr>
    <tr>
        <td>201</td>
        <td>Michael Hartstein</td>
        <td>20</td>
        <td>마케팅</td>
    </tr>
    <tr>
        <td>114</td>
        <td>Den Raphaely</td>
        <td>30</td>
        <td>구매/생산부</td>
    </tr>
    <tr>
        <td>120</td>
        <td>Matthew Weiss</td>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>121</td>
        <td>Adam Fripp</td>
        <td>50</td>
        <td>배송부</td>
    </tr>
    <tr>
        <td>103</td>
        <td>Alexander Hunold</td>
        <td>60</td>
        <td>IT</td>
    </tr>
    <tr>
        <td>204</td>
        <td>Hermann Baer</td>
        <td>70</td>
        <td>홍보부</td>
    </tr>
    <tr>
        <td>145</td>
        <td>John Russell</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>146</td>
        <td>Karen Partners</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>147</td>
        <td>Alberto Errazuriz</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>148</td>
        <td>Gerald Cambrault</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>149</td>
        <td>Eleni Zlotkey</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>150</td>
        <td>Peter Tucker</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>151</td>
        <td>David Bernstein</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>152</td>
        <td>Peter Hall</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>153</td>
        <td>Christopher Olsen</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>156</td>
        <td>Janette King</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>157</td>
        <td>Patrick Sully</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>158</td>
        <td>Allan McEwen</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>159</td>
        <td>Lindsey Smith</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>162</td>
        <td>Clara Vishney</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>163</td>
        <td>Danielle Greene</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>168</td>
        <td>Lisa Ozer</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>169</td>
        <td>Harrison Bloom</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>170</td>
        <td>Tayler Fox</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>174</td>
        <td>Ellen Abel</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>175</td>
        <td>Alyssa Hutton</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>176</td>
        <td>Jonathon Taylor</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>177</td>
        <td>Jack Livingston</td>
        <td>80</td>
        <td>영업부</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Steven King</td>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>101</td>
        <td>Neena Kochhar</td>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>102</td>
        <td>Lex De Haan</td>
        <td>90</td>
        <td>기획부</td>
    </tr>
    <tr>
        <td>108</td>
        <td>Nancy Greenberg</td>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>109</td>
        <td>Daniel Faviet</td>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>110</td>
        <td>John Chen</td>
        <td>100</td>
        <td>자금부</td>
    </tr>
    <tr>
        <td>205</td>
        <td>Shelley Higgins</td>
        <td>110</td>
        <td>경리부</td>
    </tr>
    <tr>
        <td>206</td>
        <td>William Gietz</td>
        <td>110</td>
        <td>경리부</td>
    </tr>
</table>




```sql
%%sql

SELECT AVG(c.salary) AS avg_salary
FROM
    departments b
    , employees c
WHERE b.parent_id = 90
    AND b.department_id = c.department_id
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>avg_salary</th>
    </tr>
    <tr>
        <td>7908.285714285714285714285714285714285714</td>
    </tr>
</table>


- p.200
- 2000년 이탈리아 평균 매출액(연평균)보다 큰 월의 평균 매출액은 구함
- 첫 번째 서브쿼리 : 월 평균 매출 구하는 것
- 두 번째 서브쿼리 : 연평균 매출액을 구하는 것%%sql

SELECT a.*
    FROM 
        (서브쿼리) a -- 월 평균 매출액
         , (서브쿼리) b -- 연 평균 매출액
    WHERE a.month_avg>b.year_avg  -- 연 평균 이상의 월 평균을 구한다.- 이 쿼리는 두 개의 서브 쿼리를 FROM 절에 위치시켰다. 
- 2000년 이탈리아 평균 매출액(연평균)보다 큰 달의 평균 매출액을 구해야 한다.
- 첫 번째 서브 쿼리에서는 월별 평균 매출액을, 두 번째 서브 쿼리에서는 연평균 매출액을 구한다.
  그 다음에 ‘월 평균 매출액 > 연 평균 매출액’ 조건을 만족하는 월 평균매출액을 출력한다.

```sql
%%sql

SELECT a.*
    FROM 
        (SELECT a.sales_month, ROUND(AVG(a.amount_sold)) month_avg
         FROM 
             sales a
             , customers b
             , countries c
         WHERE a.sales_month BETWEEN '200001' AND '200012'
             AND a.cust_id = b.CUST_ID
             AND b.COUNTRY_ID = c.COUNTRY_ID
             AND c.COUNTRY_NAME = 'Italy'
         GROUP BY a.sales_month ) a
        , (SELECT 
               ROUND(AVG(a.amount_sold)) AS year_avg
           FROM
               sales a
               , customers b
               , countries c
           WHERE a.sales_month BETWEEN '200001' AND '200012'
               AND a.cust_id = b.CUST_ID
               AND b.COUNTRY_ID = c.COUNTRY_ID
               AND c.COUNTRY_NAME = 'Italy') b
    WHERE a.month_avg>b.year_avg 
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>sales_month</th>
        <th>month_avg</th>
    </tr>
    <tr>
        <td>200002</td>
        <td>137</td>
    </tr>
    <tr>
        <td>200007</td>
        <td>122</td>
    </tr>
    <tr>
        <td>200009</td>
        <td>110</td>
    </tr>
    <tr>
        <td>200012</td>
        <td>184</td>
    </tr>
</table>


- ERD 참고
![ERD_000.jpg](attachment:f9c83be6-d1e8-4587-9d1e-546263376b70.jpg)
- p.200
- 복잡한 쿼리 작성법 예시
- (1), (2) --> 메인쿼리 작성
- (3), (4) --> 서브쿼리 작성 후 합치기

- 연도별로 이탈리아 매출 데이터를 살펴
- 매출실적이 가장 많은 사원의 목록과 매출액을 구하라
- 연도, 최대매출사원, 최대매출액
- 이탈리아 찾기 : countries
- 이탈리아 고객 : customers
- 매출 : sales
- 사원정보 : employees

- (1) 연도, 사원별 이탈리아 매출액 구하기
- 이탈리아 고객 찾기 : customers, countries country_id로 조인
- 이탈리아 매출 찾기 : 위 결과와 sales 테이블을 cust_id로 조인
- 최대 매출액 구하려면 MAX 함수 쓰고, 연도별로 GROUP BY


```sql
%%sql

SELECT 
    SUBSTR(a.sales_month, 1, 4) as years
    , a.employee_id
    , SUM(a.amount_sold) AS amount_sold
FROM 
    sales a
    , customers b 
    , countries c 
WHERE a.cust_id = b.cust_id
    AND b.country_id = c.country_id 
    AND c.country_name = 'Italy' 
GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>years</th>
        <th>employee_id</th>
        <th>amount_sold</th>
    </tr>
    <tr>
        <td>1998</td>
        <td>1</td>
        <td>5404.82</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>170</td>
        <td>10822.62</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>150</td>
        <td>132543.37</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>175</td>
        <td>126982.7</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>160</td>
        <td>72663.95</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>171</td>
        <td>62765.84</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>176</td>
        <td>69330.91</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>153</td>
        <td>142987.82</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>167</td>
        <td>171591.21</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>153</td>
        <td>2443.72</td>
    </tr>
    <tr>
        <td>1998</td>
        <td>156</td>
        <td>121910.05</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>168</td>
        <td>100289.54</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>172</td>
        <td>96872.2</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>169</td>
        <td>102573.99</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>145</td>
        <td>4646.74</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>163</td>
        <td>92604.53</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>179</td>
        <td>123200.62</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>149</td>
        <td>138663.65</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>154</td>
        <td>83216.54</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>176</td>
        <td>9718.24</td>
    </tr>
    <tr>
        <td>1998</td>
        <td>157</td>
        <td>203236.79</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>162</td>
        <td>94310.98</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>175</td>
        <td>24371.95</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>177</td>
        <td>90685.56</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>173</td>
        <td>426018.7</td>
    </tr>
    <tr>
        <td>1998</td>
        <td>174</td>
        <td>258841.2</td>
    </tr>
    <tr>
        <td>1998</td>
        <td>158</td>
        <td>224240.07</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>159</td>
        <td>163403.76</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>170</td>
        <td>79950.04</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>150</td>
        <td>76638.75</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>148</td>
        <td>64039.34</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>155</td>
        <td>32005</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>161</td>
        <td>53927.44</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>166</td>
        <td>141683.55</td>
    </tr>
    <tr>
        <td>1998</td>
        <td>145</td>
        <td>311761.02</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>147</td>
        <td>193319.44</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>146</td>
        <td>89197.23</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>151</td>
        <td>39957.53</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>162</td>
        <td>16259.5</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>154</td>
        <td>116769.25</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>171</td>
        <td>14145.59</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>148</td>
        <td>1557.54</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>152</td>
        <td>97859.24</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>160</td>
        <td>77893.94</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>165</td>
        <td>145408.5</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>164</td>
        <td>145790.31</td>
    </tr>
</table>


- (2) (1) 결과에서 연도별 최대, 최소 매출액 구하기

```sql
%%sql

SELECT 
    years
    , MAX(amount_sold) AS max_sold
    , MIN(amount_sold) AS min_sold
FROM (SELECT 
        SUBSTR(a.sales_month, 1, 4) as years
        , a.employee_id
        , SUM(a.amount_sold) AS amount_sold
      FROM 
        sales a
        , customers b 
        , countries c 
      WHERE a.cust_id = b.cust_id
        AND b.country_id = c.country_id 
        AND c.country_name = 'Italy' 
      GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id) K 
GROUP BY years
ORDER BY years
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>years</th>
        <th>max_sold</th>
        <th>min_sold</th>
    </tr>
    <tr>
        <td>1998</td>
        <td>311761.02</td>
        <td>5404.82</td>
    </tr>
    <tr>
        <td>1999</td>
        <td>193319.44</td>
        <td>4646.74</td>
    </tr>
    <tr>
        <td>2000</td>
        <td>142987.82</td>
        <td>16259.5</td>
    </tr>
    <tr>
        <td>2001</td>
        <td>426018.7</td>
        <td>1557.54</td>
    </tr>
</table>


- (3) (1) 결과와 (2) 결과를 조인해서
- 최대매출, 최소매출액을 일으킨 사원을 찾는다.SELECT 
    emp.years
    , emp.employee_id
    , emp.amount_sold
FROM
    () emp                 -- (1) 결과를 대입
    , () sale              -- (2) 결과를 대입
WHERE emp.years = sales.years
    AND emp.amount_sold = sale.max_sold
ORDER BY years;

```sql
%%sql


SELECT 
    emp.years
    , emp.employee_id
    , emp2.emp_name
    , emp.amount_sold
FROM 
    (SELECT 
        SUBSTR(a.sales_month, 1, 4) as years
        , a.employee_id
        , SUM(a.amount_sold) AS amount_sold
     FROM 
        sales a
        , customers b 
        , countries c 
     WHERE a.cust_id = b.cust_id
        AND b.country_id = c.country_id 
        AND c.country_name = 'Italy' 
     GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id) emp
    , (SELECT 
         years
         , MAX(amount_sold) AS max_sold
         , MIN(amount_sold) AS min_sold
         FROM (SELECT 
                 SUBSTR(a.sales_month, 1, 4) as years
                 , a.employee_id
                 , SUM(a.amount_sold) AS amount_sold
               FROM 
                sales a
                , customers b 
                , countries c 
               WHERE a.cust_id = b.cust_id
                  AND b.country_id = c.country_id 
                  AND c.country_name = 'Italy' 
               GROUP BY SUBSTR(a.sales_month, 1, 4), a.employee_id) K 
         GROUP BY years) sale
    , employees emp2
WHERE emp.years = sale.years
    AND emp.amount_sold = sale.max_sold
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
        <td>2001</td>
        <td>173</td>
        <td>Sundita Kumar</td>
        <td>426018.7</td>
    </tr>
</table>


- Reference : 오라클 SQL과 PL/SQL을 다루는 기술