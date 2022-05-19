---
title: "Oracle_practice7"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-14'
---


```python
- WINDOW Function
- 분석 함수 : 특정 그룹별 집계를 담당함
              함수의 종류

- PARTITION BY : 분석 함수로 계산될 대상 row의 그룹(파티션)을 지정
```


```python
%load_ext sql
```


```python
%sql oracle://ora_user:evan@127.0.0.1:1521/myoracle
```
- 윈도우 함수

- ROW_NUMBER()

```sql
%%sql

SELECT
    department_id
    , emp_name
    , ROW_NUMBER() OVER(PARTITION BY department_id
                        ORDER BY department_id, emp_name) dep_rows
FROM employees
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>dep_rows</th>
    </tr>
    <tr>
        <td>10</td>
        <td>Jennifer Whalen</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Michael Hartstein</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Pat Fay</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>1</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>3</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>4</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>5</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>6</td>
    </tr>
    <tr>
        <td>40</td>
        <td>Susan Mavris</td>
        <td>1</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Adam Fripp</td>
        <td>1</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alana Walsh</td>
        <td>2</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alexis Bull</td>
        <td>3</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Anthony Cabrio</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Britney Everett</td>
        <td>5</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Curtis Davies</td>
        <td>6</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Donald OConnell</td>
        <td>7</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Douglas Grant</td>
        <td>8</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Girard Geoni</td>
        <td>9</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Hazel Philtanker</td>
        <td>10</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Irene Mikkilineni</td>
        <td>11</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Landry</td>
        <td>12</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Marlow</td>
        <td>13</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jason Mallin</td>
        <td>14</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jean Fleaur</td>
        <td>15</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jennifer Dilly</td>
        <td>16</td>
    </tr>
    <tr>
        <td>50</td>
        <td>John Seo</td>
        <td>17</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Joshua Patel</td>
        <td>18</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Dellinger</td>
        <td>19</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Nayer</td>
        <td>20</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kelly Chung</td>
        <td>21</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Feeney</td>
        <td>22</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Mourgos</td>
        <td>23</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Ki Gee</td>
        <td>24</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Laura Bissot</td>
        <td>25</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Martha Sullivan</td>
        <td>26</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Matthew Weiss</td>
        <td>27</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Michael Rogers</td>
        <td>28</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Mozhe Atkinson</td>
        <td>29</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Nandita Sarchand</td>
        <td>30</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Payam Kaufling</td>
        <td>31</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Peter Vargas</td>
        <td>32</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Matos</td>
        <td>33</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Perkins</td>
        <td>34</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Renske Ladwig</td>
        <td>35</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Samuel McCain</td>
        <td>36</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Sarah Bell</td>
        <td>37</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Shanta Vollman</td>
        <td>38</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Stephen Stiles</td>
        <td>39</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Steven Markle</td>
        <td>40</td>
    </tr>
    <tr>
        <td>50</td>
        <td>TJ Olson</td>
        <td>41</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Timothy Gates</td>
        <td>42</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Trenna Rajs</td>
        <td>43</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Vance Jones</td>
        <td>44</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Winston Taylor</td>
        <td>45</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Alexander Hunold</td>
        <td>1</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Bruce Ernst</td>
        <td>2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>David Austin</td>
        <td>3</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Diana Lorentz</td>
        <td>4</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Valli Pataballa</td>
        <td>5</td>
    </tr>
    <tr>
        <td>70</td>
        <td>Hermann Baer</td>
        <td>1</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alberto Errazuriz</td>
        <td>1</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Allan McEwen</td>
        <td>2</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alyssa Hutton</td>
        <td>3</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Amit Banda</td>
        <td>4</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Charles Johnson</td>
        <td>5</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Christopher Olsen</td>
        <td>6</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Clara Vishney</td>
        <td>7</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Danielle Greene</td>
        <td>8</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Bernstein</td>
        <td>9</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Lee</td>
        <td>10</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Eleni Zlotkey</td>
        <td>11</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Elizabeth Bates</td>
        <td>12</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Ellen Abel</td>
        <td>13</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Gerald Cambrault</td>
        <td>14</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Harrison Bloom</td>
        <td>15</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jack Livingston</td>
        <td>16</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Janette King</td>
        <td>17</td>
    </tr>
    <tr>
        <td>80</td>
        <td>John Russell</td>
        <td>18</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jonathon Taylor</td>
        <td>19</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Karen Partners</td>
        <td>20</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lindsey Smith</td>
        <td>21</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lisa Ozer</td>
        <td>22</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Louise Doran</td>
        <td>23</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Mattea Marvins</td>
        <td>24</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Nanette Cambrault</td>
        <td>25</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Oliver Tuvault</td>
        <td>26</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Patrick Sully</td>
        <td>27</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Hall</td>
        <td>28</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Tucker</td>
        <td>29</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sarath Sewall</td>
        <td>30</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundar Ande</td>
        <td>31</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundita Kumar</td>
        <td>32</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Tayler Fox</td>
        <td>33</td>
    </tr>
    <tr>
        <td>80</td>
        <td>William Smith</td>
        <td>34</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Lex De Haan</td>
        <td>1</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Neena Kochhar</td>
        <td>2</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Steven King</td>
        <td>3</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Daniel Faviet</td>
        <td>1</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Ismael Sciarra</td>
        <td>2</td>
    </tr>
    <tr>
        <td>100</td>
        <td>John Chen</td>
        <td>3</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Jose Manuel Urman</td>
        <td>4</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Luis Popp</td>
        <td>5</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Nancy Greenberg</td>
        <td>6</td>
    </tr>
    <tr>
        <td>110</td>
        <td>Shelley Higgins</td>
        <td>1</td>
    </tr>
    <tr>
        <td>110</td>
        <td>William Gietz</td>
        <td>2</td>
    </tr>
    <tr>
        <td>None</td>
        <td>Kimberely Grant</td>
        <td>1</td>
    </tr>
</table>


- RANK(), DENSE_RANK()

```sql
%%sql

SELECT 
    department_id
    , emp_name
    , salary
    , RANK() OVER (PARTITION BY department_id
                   ORDER BY salary) dep_rank
    , DENSE_RANK() OVER (PARTITION BY department_id
                         ORDER BY salary) dep_denserank
FROM employees
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>salary</th>
        <th>dep_rank</th>
        <th>dep_denserank</th>
    </tr>
    <tr>
        <td>10</td>
        <td>Jennifer Whalen</td>
        <td>4400</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Pat Fay</td>
        <td>6000</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Michael Hartstein</td>
        <td>13000</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>2500</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>2600</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>2800</td>
        <td>3</td>
        <td>3</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>2900</td>
        <td>4</td>
        <td>4</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>3100</td>
        <td>5</td>
        <td>5</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>11000</td>
        <td>6</td>
        <td>6</td>
    </tr>
    <tr>
        <td>40</td>
        <td>Susan Mavris</td>
        <td>6500</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>50</td>
        <td>TJ Olson</td>
        <td>2100</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Steven Markle</td>
        <td>2200</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Hazel Philtanker</td>
        <td>2200</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Ki Gee</td>
        <td>2400</td>
        <td>4</td>
        <td>3</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Landry</td>
        <td>2400</td>
        <td>4</td>
        <td>3</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Perkins</td>
        <td>2500</td>
        <td>6</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Martha Sullivan</td>
        <td>2500</td>
        <td>6</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Joshua Patel</td>
        <td>2500</td>
        <td>6</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Peter Vargas</td>
        <td>2500</td>
        <td>6</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Marlow</td>
        <td>2500</td>
        <td>6</td>
        <td>4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Donald OConnell</td>
        <td>2600</td>
        <td>11</td>
        <td>5</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Douglas Grant</td>
        <td>2600</td>
        <td>11</td>
        <td>5</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Matos</td>
        <td>2600</td>
        <td>11</td>
        <td>5</td>
    </tr>
    <tr>
        <td>50</td>
        <td>John Seo</td>
        <td>2700</td>
        <td>14</td>
        <td>6</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Irene Mikkilineni</td>
        <td>2700</td>
        <td>14</td>
        <td>6</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Mozhe Atkinson</td>
        <td>2800</td>
        <td>16</td>
        <td>7</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Vance Jones</td>
        <td>2800</td>
        <td>16</td>
        <td>7</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Girard Geoni</td>
        <td>2800</td>
        <td>16</td>
        <td>7</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Michael Rogers</td>
        <td>2900</td>
        <td>19</td>
        <td>8</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Timothy Gates</td>
        <td>2900</td>
        <td>19</td>
        <td>8</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Feeney</td>
        <td>3000</td>
        <td>21</td>
        <td>9</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Anthony Cabrio</td>
        <td>3000</td>
        <td>21</td>
        <td>9</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jean Fleaur</td>
        <td>3100</td>
        <td>23</td>
        <td>10</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Curtis Davies</td>
        <td>3100</td>
        <td>23</td>
        <td>10</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alana Walsh</td>
        <td>3100</td>
        <td>23</td>
        <td>10</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Stephen Stiles</td>
        <td>3200</td>
        <td>26</td>
        <td>11</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Winston Taylor</td>
        <td>3200</td>
        <td>26</td>
        <td>11</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Nayer</td>
        <td>3200</td>
        <td>26</td>
        <td>11</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Samuel McCain</td>
        <td>3200</td>
        <td>26</td>
        <td>11</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Laura Bissot</td>
        <td>3300</td>
        <td>30</td>
        <td>12</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jason Mallin</td>
        <td>3300</td>
        <td>30</td>
        <td>12</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Dellinger</td>
        <td>3400</td>
        <td>32</td>
        <td>13</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Trenna Rajs</td>
        <td>3500</td>
        <td>33</td>
        <td>14</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Renske Ladwig</td>
        <td>3600</td>
        <td>34</td>
        <td>15</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jennifer Dilly</td>
        <td>3600</td>
        <td>34</td>
        <td>15</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kelly Chung</td>
        <td>3800</td>
        <td>36</td>
        <td>16</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Britney Everett</td>
        <td>3900</td>
        <td>37</td>
        <td>17</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Sarah Bell</td>
        <td>4000</td>
        <td>38</td>
        <td>18</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alexis Bull</td>
        <td>4100</td>
        <td>39</td>
        <td>19</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Nandita Sarchand</td>
        <td>4200</td>
        <td>40</td>
        <td>20</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Mourgos</td>
        <td>5800</td>
        <td>41</td>
        <td>21</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Shanta Vollman</td>
        <td>6500</td>
        <td>42</td>
        <td>22</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Payam Kaufling</td>
        <td>7900</td>
        <td>43</td>
        <td>23</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Matthew Weiss</td>
        <td>8000</td>
        <td>44</td>
        <td>24</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Adam Fripp</td>
        <td>8200</td>
        <td>45</td>
        <td>25</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Diana Lorentz</td>
        <td>4200</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Valli Pataballa</td>
        <td>4800</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>David Austin</td>
        <td>4800</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Bruce Ernst</td>
        <td>6000</td>
        <td>4</td>
        <td>3</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Alexander Hunold</td>
        <td>9000</td>
        <td>5</td>
        <td>4</td>
    </tr>
    <tr>
        <td>70</td>
        <td>Hermann Baer</td>
        <td>10000</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundita Kumar</td>
        <td>6100</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Charles Johnson</td>
        <td>6200</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Amit Banda</td>
        <td>6200</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundar Ande</td>
        <td>6400</td>
        <td>4</td>
        <td>3</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Lee</td>
        <td>6800</td>
        <td>5</td>
        <td>4</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Oliver Tuvault</td>
        <td>7000</td>
        <td>6</td>
        <td>5</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sarath Sewall</td>
        <td>7000</td>
        <td>6</td>
        <td>5</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Mattea Marvins</td>
        <td>7200</td>
        <td>8</td>
        <td>6</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Elizabeth Bates</td>
        <td>7300</td>
        <td>9</td>
        <td>7</td>
    </tr>
    <tr>
        <td>80</td>
        <td>William Smith</td>
        <td>7400</td>
        <td>10</td>
        <td>8</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Nanette Cambrault</td>
        <td>7500</td>
        <td>11</td>
        <td>9</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Louise Doran</td>
        <td>7500</td>
        <td>11</td>
        <td>9</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lindsey Smith</td>
        <td>8000</td>
        <td>13</td>
        <td>10</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Christopher Olsen</td>
        <td>8000</td>
        <td>13</td>
        <td>10</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jack Livingston</td>
        <td>8400</td>
        <td>15</td>
        <td>11</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jonathon Taylor</td>
        <td>8600</td>
        <td>16</td>
        <td>12</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alyssa Hutton</td>
        <td>8800</td>
        <td>17</td>
        <td>13</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Allan McEwen</td>
        <td>9000</td>
        <td>18</td>
        <td>14</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Hall</td>
        <td>9000</td>
        <td>18</td>
        <td>14</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Danielle Greene</td>
        <td>9500</td>
        <td>20</td>
        <td>15</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Patrick Sully</td>
        <td>9500</td>
        <td>20</td>
        <td>15</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Bernstein</td>
        <td>9500</td>
        <td>20</td>
        <td>15</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Tayler Fox</td>
        <td>9600</td>
        <td>23</td>
        <td>16</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Janette King</td>
        <td>10000</td>
        <td>24</td>
        <td>17</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Tucker</td>
        <td>10000</td>
        <td>24</td>
        <td>17</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Harrison Bloom</td>
        <td>10000</td>
        <td>24</td>
        <td>17</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Eleni Zlotkey</td>
        <td>10500</td>
        <td>27</td>
        <td>18</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Clara Vishney</td>
        <td>10500</td>
        <td>27</td>
        <td>18</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Gerald Cambrault</td>
        <td>11000</td>
        <td>29</td>
        <td>19</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Ellen Abel</td>
        <td>11000</td>
        <td>29</td>
        <td>19</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lisa Ozer</td>
        <td>11500</td>
        <td>31</td>
        <td>20</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alberto Errazuriz</td>
        <td>12000</td>
        <td>32</td>
        <td>21</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Karen Partners</td>
        <td>13500</td>
        <td>33</td>
        <td>22</td>
    </tr>
    <tr>
        <td>80</td>
        <td>John Russell</td>
        <td>14000</td>
        <td>34</td>
        <td>23</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Lex De Haan</td>
        <td>17000</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Neena Kochhar</td>
        <td>17000</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Steven King</td>
        <td>24000</td>
        <td>3</td>
        <td>2</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Luis Popp</td>
        <td>6900</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Ismael Sciarra</td>
        <td>7700</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Jose Manuel Urman</td>
        <td>7800</td>
        <td>3</td>
        <td>3</td>
    </tr>
    <tr>
        <td>100</td>
        <td>John Chen</td>
        <td>8200</td>
        <td>4</td>
        <td>4</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Daniel Faviet</td>
        <td>9000</td>
        <td>5</td>
        <td>5</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Nancy Greenberg</td>
        <td>12008</td>
        <td>6</td>
        <td>6</td>
    </tr>
    <tr>
        <td>110</td>
        <td>William Gietz</td>
        <td>8300</td>
        <td>1</td>
        <td>1</td>
    </tr>
    <tr>
        <td>110</td>
        <td>Shelley Higgins</td>
        <td>12008</td>
        <td>2</td>
        <td>2</td>
    </tr>
    <tr>
        <td>None</td>
        <td>Kimberely Grant</td>
        <td>7000</td>
        <td>1</td>
        <td>1</td>
    </tr>
</table>


- CUME_DIST & PERCENT_RANK
- CUME_DIST : 주어진 그룹에 대한 상대 누적 분포도값
- 분포도 값(비율) 반환 값의 범위 0초와 1이하 사이의 값 반환

```sql
%%sql

SELECT
    department_id
    , emp_name
    , CUME_DIST() over (PARTITION BY department_id
                        ORDER BY salary) dep_dist
FROM employees
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>dep_dist</th>
    </tr>
    <tr>
        <td>10</td>
        <td>Jennifer Whalen</td>
        <td>1</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Pat Fay</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>20</td>
        <td>Michael Hartstein</td>
        <td>1</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>0.1666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>0.3333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>0.6666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>0.8333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>1</td>
    </tr>
    <tr>
        <td>40</td>
        <td>Susan Mavris</td>
        <td>1</td>
    </tr>
    <tr>
        <td>50</td>
        <td>TJ Olson</td>
        <td>0.0222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Steven Markle</td>
        <td>0.0666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Hazel Philtanker</td>
        <td>0.0666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Ki Gee</td>
        <td>0.1111111111111111111111111111111111111111</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Landry</td>
        <td>0.1111111111111111111111111111111111111111</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Perkins</td>
        <td>0.2222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Martha Sullivan</td>
        <td>0.2222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Joshua Patel</td>
        <td>0.2222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Peter Vargas</td>
        <td>0.2222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>James Marlow</td>
        <td>0.2222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Donald OConnell</td>
        <td>0.2888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Douglas Grant</td>
        <td>0.2888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Randall Matos</td>
        <td>0.2888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>John Seo</td>
        <td>0.3333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Irene Mikkilineni</td>
        <td>0.3333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Mozhe Atkinson</td>
        <td>0.4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Vance Jones</td>
        <td>0.4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Girard Geoni</td>
        <td>0.4</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Michael Rogers</td>
        <td>0.4444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Timothy Gates</td>
        <td>0.4444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Feeney</td>
        <td>0.4888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Anthony Cabrio</td>
        <td>0.4888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jean Fleaur</td>
        <td>0.5555555555555555555555555555555555555556</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Curtis Davies</td>
        <td>0.5555555555555555555555555555555555555556</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alana Walsh</td>
        <td>0.5555555555555555555555555555555555555556</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Stephen Stiles</td>
        <td>0.6444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Winston Taylor</td>
        <td>0.6444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Nayer</td>
        <td>0.6444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Samuel McCain</td>
        <td>0.6444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Laura Bissot</td>
        <td>0.6888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jason Mallin</td>
        <td>0.6888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Julia Dellinger</td>
        <td>0.7111111111111111111111111111111111111111</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Trenna Rajs</td>
        <td>0.7333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Renske Ladwig</td>
        <td>0.7777777777777777777777777777777777777778</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Jennifer Dilly</td>
        <td>0.7777777777777777777777777777777777777778</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kelly Chung</td>
        <td>0.8</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Britney Everett</td>
        <td>0.8222222222222222222222222222222222222222</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Sarah Bell</td>
        <td>0.8444444444444444444444444444444444444444</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Alexis Bull</td>
        <td>0.8666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Nandita Sarchand</td>
        <td>0.8888888888888888888888888888888888888889</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Kevin Mourgos</td>
        <td>0.9111111111111111111111111111111111111111</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Shanta Vollman</td>
        <td>0.9333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Payam Kaufling</td>
        <td>0.9555555555555555555555555555555555555556</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Matthew Weiss</td>
        <td>0.9777777777777777777777777777777777777778</td>
    </tr>
    <tr>
        <td>50</td>
        <td>Adam Fripp</td>
        <td>1</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Diana Lorentz</td>
        <td>0.2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Valli Pataballa</td>
        <td>0.6</td>
    </tr>
    <tr>
        <td>60</td>
        <td>David Austin</td>
        <td>0.6</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Bruce Ernst</td>
        <td>0.8</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Alexander Hunold</td>
        <td>1</td>
    </tr>
    <tr>
        <td>70</td>
        <td>Hermann Baer</td>
        <td>1</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundita Kumar</td>
        <td>0.0294117647058823529411764705882352941176</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Charles Johnson</td>
        <td>0.0882352941176470588235294117647058823529</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Amit Banda</td>
        <td>0.0882352941176470588235294117647058823529</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sundar Ande</td>
        <td>0.1176470588235294117647058823529411764706</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Lee</td>
        <td>0.1470588235294117647058823529411764705882</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Oliver Tuvault</td>
        <td>0.2058823529411764705882352941176470588235</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Sarath Sewall</td>
        <td>0.2058823529411764705882352941176470588235</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Mattea Marvins</td>
        <td>0.2352941176470588235294117647058823529412</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Elizabeth Bates</td>
        <td>0.2647058823529411764705882352941176470588</td>
    </tr>
    <tr>
        <td>80</td>
        <td>William Smith</td>
        <td>0.2941176470588235294117647058823529411765</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Nanette Cambrault</td>
        <td>0.3529411764705882352941176470588235294118</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Louise Doran</td>
        <td>0.3529411764705882352941176470588235294118</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lindsey Smith</td>
        <td>0.4117647058823529411764705882352941176471</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Christopher Olsen</td>
        <td>0.4117647058823529411764705882352941176471</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jack Livingston</td>
        <td>0.4411764705882352941176470588235294117647</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Jonathon Taylor</td>
        <td>0.4705882352941176470588235294117647058824</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alyssa Hutton</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Allan McEwen</td>
        <td>0.5588235294117647058823529411764705882353</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Hall</td>
        <td>0.5588235294117647058823529411764705882353</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Danielle Greene</td>
        <td>0.6470588235294117647058823529411764705882</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Patrick Sully</td>
        <td>0.6470588235294117647058823529411764705882</td>
    </tr>
    <tr>
        <td>80</td>
        <td>David Bernstein</td>
        <td>0.6470588235294117647058823529411764705882</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Tayler Fox</td>
        <td>0.6764705882352941176470588235294117647059</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Janette King</td>
        <td>0.7647058823529411764705882352941176470588</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Peter Tucker</td>
        <td>0.7647058823529411764705882352941176470588</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Harrison Bloom</td>
        <td>0.7647058823529411764705882352941176470588</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Eleni Zlotkey</td>
        <td>0.8235294117647058823529411764705882352941</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Clara Vishney</td>
        <td>0.8235294117647058823529411764705882352941</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Gerald Cambrault</td>
        <td>0.8823529411764705882352941176470588235294</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Ellen Abel</td>
        <td>0.8823529411764705882352941176470588235294</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Lisa Ozer</td>
        <td>0.9117647058823529411764705882352941176471</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Alberto Errazuriz</td>
        <td>0.9411764705882352941176470588235294117647</td>
    </tr>
    <tr>
        <td>80</td>
        <td>Karen Partners</td>
        <td>0.9705882352941176470588235294117647058824</td>
    </tr>
    <tr>
        <td>80</td>
        <td>John Russell</td>
        <td>1</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Lex De Haan</td>
        <td>0.6666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Neena Kochhar</td>
        <td>0.6666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>90</td>
        <td>Steven King</td>
        <td>1</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Luis Popp</td>
        <td>0.1666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Ismael Sciarra</td>
        <td>0.3333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Jose Manuel Urman</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>100</td>
        <td>John Chen</td>
        <td>0.6666666666666666666666666666666666666667</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Daniel Faviet</td>
        <td>0.8333333333333333333333333333333333333333</td>
    </tr>
    <tr>
        <td>100</td>
        <td>Nancy Greenberg</td>
        <td>1</td>
    </tr>
    <tr>
        <td>110</td>
        <td>William Gietz</td>
        <td>0.5</td>
    </tr>
    <tr>
        <td>110</td>
        <td>Shelley Higgins</td>
        <td>1</td>
    </tr>
    <tr>
        <td>None</td>
        <td>Kimberely Grant</td>
        <td>1</td>
    </tr>
</table>


- NTILE 함수
- NTILE(4) 값을 4등분 함

```sql
%%sql

SELECT 
    department_id
    , emp_name
    , salary
    , NTILE(4) OVER (PARTITION BY department_id
                     ORDER BY salary) NTILES
FROM employees
WHERE department_id IN (30, 60)
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>department_id</th>
        <th>emp_name</th>
        <th>salary</th>
        <th>ntiles</th>
    </tr>
    <tr>
        <td>30</td>
        <td>Karen Colmenares</td>
        <td>2500</td>
        <td>1</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Guy Himuro</td>
        <td>2600</td>
        <td>1</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Sigal Tobias</td>
        <td>2800</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Shelli Baida</td>
        <td>2900</td>
        <td>2</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Alexander Khoo</td>
        <td>3100</td>
        <td>3</td>
    </tr>
    <tr>
        <td>30</td>
        <td>Den Raphaely</td>
        <td>11000</td>
        <td>4</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Diana Lorentz</td>
        <td>4200</td>
        <td>1</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Valli Pataballa</td>
        <td>4800</td>
        <td>1</td>
    </tr>
    <tr>
        <td>60</td>
        <td>David Austin</td>
        <td>4800</td>
        <td>2</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Bruce Ernst</td>
        <td>6000</td>
        <td>3</td>
    </tr>
    <tr>
        <td>60</td>
        <td>Alexander Hunold</td>
        <td>9000</td>
        <td>4</td>
    </tr>
</table>


- LAG : 선행 로우의 값을 참조한다.
- LEAD : 후행 로우의 값 참조

```sql
%%sql

SELECT 
    emp_name
    , hire_date
    , salary
    , LAG(salary, 1, 0) OVER (ORDER BY hire_date) AS prev_sal
    , LEAD(salary, 1, 0) OVER (ORDER BY hire_date) AS next_sal
FROM employees
WHERE department_id = 30
```

     * oracle://ora_user:***@127.0.0.1:1521/myoracle
    0 rows affected.
    




<table>
    <tr>
        <th>emp_name</th>
        <th>hire_date</th>
        <th>salary</th>
        <th>prev_sal</th>
        <th>next_sal</th>
    </tr>
    <tr>
        <td>Den Raphaely</td>
        <td>2002-12-07 00:00:00</td>
        <td>11000</td>
        <td>0</td>
        <td>3100</td>
    </tr>
    <tr>
        <td>Alexander Khoo</td>
        <td>2003-05-18 00:00:00</td>
        <td>3100</td>
        <td>11000</td>
        <td>2800</td>
    </tr>
    <tr>
        <td>Sigal Tobias</td>
        <td>2005-07-24 00:00:00</td>
        <td>2800</td>
        <td>3100</td>
        <td>2900</td>
    </tr>
    <tr>
        <td>Shelli Baida</td>
        <td>2005-12-24 00:00:00</td>
        <td>2900</td>
        <td>2800</td>
        <td>2600</td>
    </tr>
    <tr>
        <td>Guy Himuro</td>
        <td>2006-11-15 00:00:00</td>
        <td>2600</td>
        <td>2900</td>
        <td>2500</td>
    </tr>
    <tr>
        <td>Karen Colmenares</td>
        <td>2007-08-10 00:00:00</td>
        <td>2500</td>
        <td>2600</td>
        <td>0</td>
    </tr>
</table>


- Reference : 오라클 SQL과 PL/SQL을 다루는 기술