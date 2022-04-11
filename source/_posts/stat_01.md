---
title: "R 통계분석"
tags:
  - R
  - R Markdown
categories:
  - R
  - 분석 방법
author: "minkuen"
date: '2022-03-21'
output:
  html_document:
    keep_md: true
---


### ***해당 글은 "R을 이용한 공공데이터 분석"책의 8장을 정리한 글입니다. 

# [ 1. 분석 방법 ]

### 기술 통계

- 평균, 최솟값, 최댓값, 중앙값과 같이 데이터의 특징을 알려주는 값
- 기술통계는 Descriptive statistic

### 추론 통계

- 변수 간의 관계를 파악하고, 변수간의 인과관계 또는 새로운 사실을 밝혀냄
- 평균 차이 검정, 교차 분석, 상관관계분석, 회귀분석

### 평균차이 검정

- 집단별로 평균의 차이가 실제로 있는가 검정
- 독립표본 T검정

### 교차분석

- 범주형 변수로 구성된 집단들의 관련성을 검정하는 통계 분석
- 교차분석은 카이제곱(x^2)검정, 카이스퀘어검정, 독립성 검정이라고도 함

### 상관관계분석

- 상관관계분석은 변수 간의 상관관계(correlation)를 알아보는 것
- 변수간의 연관성
- 한 변수가 변화하면 다른 변수도 변화하는 관계
- 방향은 한 변수가 변화할 때 다른 변수가 같은 방향으로 변화하는지, 반대 방향으로 변화하는지를 의미
- 변화의 강도와 방향을 나나나는 계수가 상관계수(r)
- 상관계수는 -1~1 사이에 있으며, 수치가 클수록 영향을 주는 강도가 크다
- '+'는 '정의 관계', '-'는 '부의 관계' 또는 '역의 관계'에 있는 것을 의미
- 상관관계 : -1 <= r <= 1

### 회귀분석

- 상관관계로는 변수들의 관계를 알 수 있지만, 인과관계는 알 수 없음
- 인과관계는 원인과 결과의 관계. 한 변수가 다른 변수에 영향을 주는 것
- 영향을 주는 변수는 독립변수(independent variable)이고, 
  영향을 받는 변수는 종속변수(dependent variable)이다
- 독립변수와 종속변수 간의 인과관계를 분석하는 통계적 방법을
  회귀분석(regression analysis)이라고 한다
- "월급이 증가하면 외식횟수가 늘어날 것"이라고 가정하면, 월급은 독립변수이고 외식횟수는 종속변수이다
- 월급의 증감이 외식횟수에 미치는 영향을 확률적으로 분석하는 것이 회귀분석
- 회귀분석에서 독립변수가 1개이면 단순회귀분석, 2개 이상이면 다중회귀분석이라고 함
- 다중회귀분석은 종속 변수는 1개이며 독립변수가 복수인 경우
- 복수의 독립변수들이 종속변수에 영향을 주는 정도를 분석하는 것


# [ 2. 통계 검정 ]

### 가설

- 가설(hypothesis)은 어떤 현상을 설명하기 위해 가정하는 명제
- 증명되지 않은 추정
- 가설에는 귀무가설과 대립가설이 있다
- 귀무가설은 설정한 가설이 맞을 확률이 극히 적어서 처음부터 기각될 것으로 예상되는 가설
- 대립가설은 귀무가설이 기각될 경우 받아들여지는 가설이며, 연구자가 검정하고자 하는 가설
- 통계 검정은 통계적인 방법을 이용해서 대립가설이 맞는가를 검정하는 것
- 두 집단의 평균 차이가 있는가를 알아보려 할 때, 귀무가설은 '평균 차이가 없다'이며, 대립 가설은 '평균 차이가 있다'이다.

### 유의수준

- 가설검정의 결과는 유의수준에 의하여 결정
- 유의수준(significance level)은 귀무가설이 맞는데도 대립가설을 체택할 확률
- 즉 오류를 범할 확률. 차이가 없는 데도 있다고 할 확률이다
- 통계 분석에서는 p-value(p값)f로 제시
- p값이 0.01이라면 오류를 범할 확률이 1%라는 의미
- 현실적으로 오류는 존재할 수 밖에 없기에, '허용할 수 있는 오류 범위'를 설정
- 유의수준 5%는 오류를 5%까지 허용하겠다는 의미
- 허용하는 유의수준의 범위와 정확성은 반대의 개념
- 유의수준의 범위가 넓으면 연구 결과를 얻기가 쉽지만 결과의 정확성이 떨어진다
- 통계분석을 하면 결과물에는 유의수준(p-value)이 적혀있다
- 통계 분석 결과를 해석할 때는 먼저 유의수준이 0.05 이내인가를 보고, 결과가 통계적으로 유의미한지를 판단해야 한다
- 유의수준이 0.05 이상인데도 결과가 유의미하다고 해석하면 매우 심각한 오류.
- 유의수준의 반대 개념은 신뢰수준(confidence level). 신뢰할 수 있는 범위를 의미.
- 유의수준 5% 이내라고 하면 신뢰수준은 95%

### 척도

- 척도(scale)는 측정도구이며, 수치로 표시된다
- 척도에는 명목척도, 서열척도, 등간척도, 비율척도 등 네 종류가 있다
- 명목척도 : 측정대상의 특성이나 범주를 구분하는 수치. 운동선수의 번호를 생각하면 파악하기 쉽다.
             번호는 특정 선수를 의미. 성을 분류할 때 통상 남자를 1번, 여자를 2번으로 분류하는 것과 같이
             결혼유무, 종교, 인종, 지역, 계절 등을 표시할 때도 이용된다. 산술연산을 할 수 없다.
- 서열척도 : 계급, 사회계층, 자격등급 등과 같이 측정대상의 등급순위를 나타내는 척도. 척도 간의 거리나 간격은 나타내지 않는다. 산술연산을 할 수 없다.
- 등간척도 : 측정대상을 일정한 간격으로 구분한 척도이다. 서열뿐만 아니라 거리와 간격도 표시한다.
             온도, 학력, 시험점수 등. 덧셈과 뺄셈이 가능.
- 비율척도 : 측정대상을 비율로 나타낼 수 있는 척도. 연령, 무게 등. 모든 수로 측정할 수 있어
             4칙 연산이 가능.


# [ 3. 통계 분석 사례 ]

### 두 집단의 평균 차이 검정

- 남녀 등 두 집단의 평균 차이를 분석할 때는 독립표본 t검정을 한다
- R에서는 내장된 t.test()함수로 한다
- 독립변수는 명목척도이며, 종속변수는 등간척도 또는 비율척도이어야 한다.
- t.test()함수 사용 방식은 2가지
  방법1. t.test(data=데이터세트,종속변수(비교값) ~ 독립변수(비교대상))
  방법2. t.test(데이터세트$종속변수(비교값) ~ 데이터세트$독립변수(비교대상))

- 예제파일인 mpg1.csv의 trans변수에는 기어변속방법으로 auto(자동식)와 manual(수동식)등 두 방식이 있다.
  두 방식에 cty 평균에 통계적으로 유의미한 차이가 있는지 알아보자.
  cty는 도시에서 1갤런당 달리는 거리.
  독립변수는 trans이며, 종속변수는 cty이다. 
  가설은 다음과 같이 설정한다.
  
  - 귀무가설(H0) : auto와 manual의 cty평균은 차이가 없다.
  - 대립가설(H1) : auto와 manual의 cty평균은 차이가 있다.

```r
mpg1 <- read.csv("mpg1.csv")
t.test(data=mpg1, cty~trans) #t.test(mpg1$cty~mpg1$tran)도 같음
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  cty by trans
## t = -4.5375, df = 132.32, p-value = 1.263e-05
## alternative hypothesis: true difference in means between group auto and group manual is not equal to 0
## 95 percent confidence interval:
##  -3.887311 -1.527033
## sample estimates:
##   mean in group auto mean in group manual 
##             15.96815             18.67532
```
  - 결과를 보면 p-value=1.263e-05 임을 알 수 있으며 이 값은 1.263/100000 < 0.05 이다.
    유의수준이 0.05보다 적기 때문에 유의수준 허용조건(p<.05)을 총종한다.
    결과의 'alternative hypothesis : true difference in means is not equal to 0'는
    '대립가설 : 평균 차이가 있다' 라는 의미.
    
### 교차분석

- 교차분석은 범주형 변수들이 관계가 있다는 것을 입증하는 것
- 평균의 차이가 아니라, 비율에 차이가 있는지를 검정
- 교차분석 검정은 R의 chisq.test() 함수 사용

- mpg1.csv를 mpg1로 불러온다. mpg1에 있는 trans(기어 변속방식)변수의 범주에 따라 drv(구동방식)
  범주의 비율에 차이가 있는가를 알아본다. 연구가설은 다음과 같이 설정.
    - 귀무가설(H0) : trans에 따라 drv의 차이가 없다.
    - 대립가설(H1) : trans에 따라 drv의 차이가 있다.
  
  우선 table() 함수와 prop.table()함수로 교차분석을 해서 trans에 따른 drv의 빈도와 비율을 알아본다.

```r
mpg1 <- read.csv("mpg1.csv", stringsAsFactors = F)

table(mpg1$trans, mpg1$drv) # trans와 drv의 교차분석
```

```
##         
##           4  f  r
##   auto   75 65 17
##   manual 28 41  8
```

```r
prop.table(table(mpg1$trans, mpg1$drv),1) # auto와 manual의 drv 비율 분석
```

```
##         
##                  4         f         r
##   auto   0.4777070 0.4140127 0.1082803
##   manual 0.3636364 0.5324675 0.1038961
```
  - auto에서는 4륜구동(4)인 47.8%로 가장 많고, manual에서는 전륜구동(f)이 53.2%이 가장 많아서
    trans에 따라 drv에 차이가 있는 것 같다. 이에 대해 정말 그런지, 통계적으로 분석하는 것이 교차분석이다.
    
  - 방법 1

```r
chisq.test(mpg1$trans, mpg1$drv)
```

```
## 
## 	Pearson's Chi-squared test
## 
## data:  mpg1$trans and mpg1$drv
## X-squared = 3.1368, df = 2, p-value = 0.2084
```
    
  - 방법 2

```r
chisq.test(table(mpg1$trans, mpg1$drv))
```

```
## 
## 	Pearson's Chi-squared test
## 
## data:  table(mpg1$trans, mpg1$drv)
## X-squared = 3.1368, df = 2, p-value = 0.2084
```
  
  - 방법 3

```r
summary(table(mpg1$trans, mpg1$drv))
```

```
## Number of cases in table: 234 
## Number of factors: 2 
## Test for independence of all factors:
## 	Chisq = 3.1368, df = 2, p-value = 0.2084
```
  - 방법 1의 결과를 보면 유의수준(p-value)이 0.2084 > 0.5 이다. 대립가설을 기각하지 못하므로
    trans에 따라 drv에 차이가 있다고 할 수 없다. 다른 방법에서도 같은 결과.
  
### 상관관계분석

- 상관관계분석은 R에 내장되어 있는 cor.test()함수로 한다

```r
#cor.test(데이터세트$비교변수1, 데이터세트$비교변수2)
```

- mpgl에는 cty와 hwy가 있다
- cty는 도시에서 1갤런당 달리는 거리
- hwy는 고속도로에서 1갤런당 달리는 거리

- cty가 길면 hwy도 길 것이라 생각할 수 있다. 이 가설을 검정해본다.
  검정하려는 가설은 cty와 hwy는 서로 상관관계가 있다는 것이기 때문에 이것이 대립가설.
  귀무가설은 상관관계가 없다는 것이다.
  
  - 귀무가설(H0) : cty와 hwy는 상관관계가 없다.
  - 대립가설(H1) : cty와 hwy는 상관관계가 있다.

```r
mpg1 <- read.csv("mpg1.csv", stringsAsFactors = F)

cor.test(mpg1$cty, mpg1$hwy) #상관관계분석
```

```
## 
## 	Pearson's product-moment correlation
## 
## data:  mpg1$cty and mpg1$hwy
## t = 49.585, df = 232, p-value < 2.2e-16
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.9433129 0.9657663
## sample estimates:
##       cor 
## 0.9559159
```
  - 결과를 보면 'p-value < 2.2e-15'이다. 유의수준이 2.2/10^16보다 작다.
    유의수준(p<.05)안에 있다. 이 검정의 결과로 귀무가설을 기각하고 대립가설을 채택할 수 있다.
    대립가설은 "상관관계는 0이 아니다(alternative hypothesis: true correlation is not equal to 0)"
    
  - 결과의 sample estimates: 부분을 보면 상관관계는 0.9959159. 1에 가까우므로 매우 높다.
    결과는 "cty와 hwy는 유의미하게 매우 높은 상관관계(r=.96)에 있다(p>.05)"

### 회귀분석

### 단순회귀분석

- 단순회귀분석은 독립변수가 1개, 종속변수가 1개일때 한다
- 회귀분석의 변수는 독립변수와 종속변수가 모두 등간척도 또는 비율척도이어야 한다
- 회귀분석은 R의 lm() 함수로 한다

```r
#다음 3가지 중 어느 것을 써도 된다.
#방법1  lm(data=데이터세트, 종속변수~독립변수)
#방법2  lm(종속변수~독립변수, data=데이터세트)
#방법3  lm(데이터세트$종속변수~데이터세트$독립변수)
```

- R에 있는 mtcars 데이터로 분석한다. R에서 help(mtcars)를 하면 mtcars에 관한 정보를 알 수 있다.
  어느 한 미국 잡지에 실렸던 데이터이며, 11개 변수에서 32개 자동차의 정보를 담고 있다. 
  11개의 변수 가운데 disp(배기량)가 mpg(1갤런당 주행 마일)에 미치는 여향을 분석해본다.
  str(mtcars)로 mtcars에 있는 변수들을 보면, disp와 mpg는 모두 실수형(num)변수이어서 회귀분석이 가능하다.
  
  - 귀무가설(H0) : disp는 mpg에 영향을 주지 않는다.
  - 귀무가설(H1) : disp는 mpg에 영향을 준다.

```r
lm(data=mtcars, mpg~disp)
```

```
## 
## Call:
## lm(formula = mpg ~ disp, data = mtcars)
## 
## Coefficients:
## (Intercept)         disp  
##    29.59985     -0.04122
```

```r
#lm(mpg~disp, data=mtcars), lm(mtcars$mpg~mtcars$disp)의 결과도 같다.
```
  - 결과의 Coefficients 부분을 보면 disp의 계수(Coefficients)는 -0.04122이며, 절편은 29.59985이다.
    단순회귀분석은 1차 함수를 구하는 것과 같다.
    이 회귀분석에서 구해진 식은 mpg는 0.04122씩 감소한다.
    이제 유의수준을 알아봐야 한다. lm()의 결과를 summary()함수에 넣으면 상세한 결과를 확인 가능.

```r
RA <- lm(data=mtcars, mpg~disp) #회귀분석 결과를 RA에 넣기

summary(RA) # 상세한 분석 결과 출력
```

```
## 
## Call:
## lm(formula = mpg ~ disp, data = mtcars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -4.8922 -2.2022 -0.9631  1.6272  7.2305 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 29.599855   1.229720  24.070  < 2e-16 ***
## disp        -0.041215   0.004712  -8.747 9.38e-10 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.251 on 30 degrees of freedom
## Multiple R-squared:  0.7183,	Adjusted R-squared:  0.709 
## F-statistic: 76.51 on 1 and 30 DF,  p-value: 9.38e-10
```
  
  - 결과의 맨 밑줄을 확인하면 통계분석을 한 회귀모형이 적합한가를 순석하는 값이 있다.
  - p-value가 .05보다 작으면 회귀모형이 적합하다고 해석한다.
  - p-value가 .05보다 크면 회귀모형에 문자가 있는 것이므로 회귀분석 자체가 성립하지 않는다.
  - 이 분석에서는 p-value가 9.38e-10이므로 회귀모형이 적합하다.
  
### 다중회귀분석

- 다중회귀분석은 종속변수에 영향을 주는 독립변수가 복수일 때 분석하는 방식이다.
- 여러 독립변수들은 서로 영향을 주면서 종속변수에 영향을 주기 때문에
  한 독립변수가 종속변수에 미치는 영향력은 단순회귀분석을 했을 때와 다중회귀 분석을 했을 때에 달라진다.
- 다중회귀분석에서는 단순회귀분석의 독립변수들을 '+'기호로 연결한다.

```r
#방법1  lm(data=데이터세트, 종속변수~독립변수1+독립변수2+...)
#방법2  lm(종속변수~독립변수1+독립변수2+..., data=데이터세트)
#방법3  lm(데이터세트$종속변수~데이터세트$독립변수1+데이터세트$독립변수2+...)
```

- mtcars 데이터로 실습한다. mpg에는 disp(배기량)이외에도 hp(마력)와 wt(중량)가 영향을 미칠 수 있다.
  세 독립변수가 mpg에 어떤 영향을 주는지 알아본다.

```r
lm(data=mtcars, mpg~disp+hp+wt)
```

```
## 
## Call:
## lm(formula = mpg ~ disp + hp + wt, data = mtcars)
## 
## Coefficients:
## (Intercept)         disp           hp           wt  
##   37.105505    -0.000937    -0.031157    -3.800891
```

```r
#lm(mpg~disp+hp+wt, data=mtcars),
#lm(mtcars$mpg~mtcars$disp+mtcars$hp+mtcars$wt)의 결과도 같다.
```

- 결과의 Coefficients 부분을 보면 세 독립변수의 회귀계수가 있다.
  다중회귀식은 mpg = 37.105505 - 0.000937 x disp - 0.0311157 x hp - 0.3800891 x wt이다. 
  그러나 세 독립변수의 회귀계수에 대한 유의수준이 없어서 회귀계수가 유의미한지 알 수 없다.
  summary()함수로 유의수준을 비롯한 상세 결과를 알아본다.
  

```r
RA <- lm(data=mtcars, mpg~disp+hp+wt) #회귀분석 결과를 RA 녛기

summary(RA)
```

```
## 
## Call:
## lm(formula = mpg ~ disp + hp + wt, data = mtcars)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -3.891 -1.640 -0.172  1.061  5.861 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 37.105505   2.110815  17.579  < 2e-16 ***
## disp        -0.000937   0.010350  -0.091  0.92851    
## hp          -0.031157   0.011436  -2.724  0.01097 *  
## wt          -3.800891   1.066191  -3.565  0.00133 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.639 on 28 degrees of freedom
## Multiple R-squared:  0.8268,	Adjusted R-squared:  0.8083 
## F-statistic: 44.57 on 3 and 28 DF,  p-value: 8.65e-11
```
  
- 결과의 맨 밑줄을 확인하면 p값은 86e-11로 유의수준 .001보다 작아 회귀모형은 적합하다
- Coefficients 부분을 보면 각각의 유의수준은 disp는 (p>.05), hp는 (p<.05), wt는 (p<.01)이다
- disp는 mpg에 영향을 주지 않고, hp와 wt만 영향을 준다
- 결과의 Adjusted R-squared 는 0.8083으로 높아서 회귀모델의 설명력이 높다
- 위 내용들을 토대로 다음과 같이 적는다
    - "회귀모형은 유의수준 p<.001에서 적합하며, 회귀식의 수정된 결정계수(R^2)는 .81이다. 
      3개 독립변수가 연비에 미치는 회귀계수(베타)는 hp가 -0.03(p<.05), wt가 -3.80(p<.01), disp는 없다.
      wt의 영향력이 가장 컸다."

- Reference : R을 이용한 공공데이터 분석

# End of Document

