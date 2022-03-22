---
title: "Java Script"
tags:
  - JavaScript
  - Notion
  - 생활코딩
categories:
  - JavaScript
  - 생활코딩
author: "minkuen"
date: '2022-03-21'
---


### 유튜브 영상인 ‘자바스크립트 입문’ 영상을 정리한 글입니다.

[JavaScript - 오리엔테이션 - YouTube](https://www.youtube.com/watch?v=PZIPsKgWJiw&list=PLuHgQVnccGMA4uSig3hCjl7wTDeyIeZVU)

*참고 - 생활코딩 링크

[https://opentutorials.org/course/1](https://opentutorials.org/course/1)


=1번 영상============================================

[프로그래밍이란 무엇인가]

자바스크립트 = 웹브라우저 제작 가능한 언어

탈웹브라우저의 흐름  →  자바스크립트를 웹서버에서 사용

웹서버를 동작하는 도구로서의 자바스크립트 = 서버 사이드 스크립트

node.js = 서버 사이드 스크립트의 대표적 기술.

자바스크립트는 웹브라우저에서 동작하지만 시간이 흘러

자바스크립트를 웹서버에서 동작하게 하는 기술이 등장.

이 기술의 예시로는 PHP, JAVA, PYTHON, Node.js 등이 있으며

 이중에서도 각광받고 있는 기술이 Node.js 이다.

![Untitled](/images/java_Script/Untitled.png)

또 하나의 자바스크립트의 중요한 흐름은 탈웹.

웹 밖에서도 자바스크립트가 사용되기 시작.

이 예시로는 google apps script가 있다.

언어 = 의사소통을 위한 ‘약속’

자바스크립트의 작동 환경 → 웹브라우저, nod.js, spreadSheet

![Untitled](/images/java_Script/Untitled%201.png)

웹브라우저에서 alert가 작동하고

node.js에서 write가 사용되며

spreadSheet 에서 msgBox가 이용됨.


=2번 영상============================================

[언어의 실행방법과 실습환경에 대해서 알아본다]

기본 에디터를 사용하여 자바스크립트를 실행하는 법을 공부. 

윈도우 기준 → 텍스트에디터 =  메모장 사용

 

링크를 타고 해당 내용을 복사 붙여넣기.

`<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"/>
</head>
<body>
<script>
alert('Hello world');   →>>>> 이 부분만 자바스크림트 / 나머진 html.
</script>
</body>
</html>`

+→ alert 명령어는 경고창 형태로 띄우는 기능.

다른 이름으로 저장하기 → sample.html → 파일형식:모든 파일 → 인코딩:UTF-8

![Untitled](/images/java_Script/Untitled%202.png)

[https://opentutorials.org/module/532/4646](https://opentutorials.org/module/532/4646)

해당 링크를 참고하라.


=3번 영상============================================

Chrome 크롬 브라우저 기준으로 설명.

개발자 도구를 킵니다 : 웹 브라우저 → 도구 → 개발자 도구 

자바스크립트를 입력합니다 : 개발자 도구 → console → 자바스크립트 입력

더 자세한 정보는 해당 링크를 참고.

[https://opentutorials.org/course/580](https://opentutorials.org/course/580)

`<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"/>
</head>
<body>
<script>
console.log('Hello world');  →>>> 개발자 도구의 콘솔에 hello world 출력됨. 
</script>
</body>
</html>`

해당 내용으로 메모장을 수정하고 저장만 하면 적용됨.


=4번 영상============================================

도구의 선택.

IDE = 통합 개발 환경

운영 체제에 맞는 IDE 를 사용해야 한다.

좋은 개발 도구를 사용하는 것은 좋은 코드를 작성하는 것만큼 중요.

[https://opentutorials.org/module/406/3595](https://opentutorials.org/module/406/3595)


=5번 영상============================================

숫자와 문자 : 수의 표현

sublime Text를 설치.

파일 목록 표시 : view → show side view

사용할 파일 지정? : project → open project

입력할 창 생성 : 폴더에 우클릭 → new file

내용 입력 : 1. html 입력 후 Tab 키 = 기본적인 내용이 채워짐.

                   2. 빈 부분에 script 입력 후 Tab 키 = 추가로 내용이 채워짐.

                   3. 다음 캡처와 같이 정리하고 빈 칸에 원하는 내용 입력.

![Untitled](/images/java_Script/Untitled%203.png)

자바스크립트 입력 후 저장하면 적용된다.

ex) alert(1);   alert(1.1);   alert(1.1+1.1);  alert(2*8)

1 → 정수

1.1 → 실수

![Untitled](/images/java_Script/Untitled%204.png)

개발자 도구의 콘솔에서도 계산 가능.


=6번 영상============================================

수학 관련 명령어

수학 함수 Math 소개.

Math.pow(3,2);        →>>>  3의 제곱은 9라는 내용.

→ 9

Math.round(10.6);   →>>> 10.6의 반올림

→11

 Math.ceil(10.2);      →>>> 10.2의 올림.

→11

Math.floor(10.2);     →>>> 10.2의 내림.

→ 10

Math.sqrt(9)        →>>> 9의 제곱근.

→3

Math.random();    →>>> 1보다 작은 랜덤 실수.

100 * Math.random();   →>>> 100보다 작은 랜덤 실수.

Math.round( 100 * Math.random() ); →>>> 100 보다 작은 랜덤 정수


=7번 영상============================================

따옴표 사용.

따옴표 = 지금부터 작성하는 것은 문자임

작은 따옴표로 열은 문장은 작은 따옴표로 닫아야 한다.

큰 따옴표로 열은 문장은 큰 따옴표로 닫아야 한다.

![Untitled](/images/java_Script/Untitled%205.png)

*작은 따옴표 내에서 작은 따옴표 사용하기 ⇒ 역 슬래쉬 사용 ⇒   \  (escape)

*따옴표 내에 있다면 숫자라도 문자 취급 ⇒ ‘1’ 은 문자이다.

                                                                       따라서  ‘1’+’1’ = ‘11’ 이다.

*타입 구분법 ⇒ typeof

ex) typeof 1,   typeof ‘1’


=8번 영상============================================

개행 사용법.

개행 = 줄바꿈이란 의미 ⇒ \n

공백 생성법  ⇒   “  “ 와  +  를 사용.

 ex) “coding” + “  “ + “everyday   ⇒  coding  everyday

길이 측정법 ⇒ length 를 사용

ex) “coding everybody”.length = 16

*자바스크립트 명령어 모음.

다음 링크를 참고하라.

[https://opentutorials.org/course/50/37](https://opentutorials.org/course/50/37)

문자 위치 출력 ⇒ indexOf 를 사용

ex) “code”.indexOf(”c”)=0, “code”.indexOf(”o”)=1,

     “code”.indexOf(”d”)=2, “code”.indexOf(”e”)=3


=9번 영상============================================

변수.

변수 선언 예시 ⇒    var a = 1;  

다음 같이 시행하면 경고창으로 10 이 출력된다.

![Untitled](/images/java_Script/Untitled%206.png)

다음과 같이 문자로도 사용 가능하다.

![Untitled](/images/java_Script/Untitled%207.png)


=10번 영상===========================================

[변수의 효용]

변수의 값을 바꾸면 해당 변수가 들어간 모든 식에 반영이 된다.

이것은 매우 편리하고 실용적인 기능이다. 변수를 쓰는 이유 중 하나이다.

변수 사용 팁 ⇒ 여러 줄로 이루어진 식이 있다면

                          변할 수 있는 부분과 변하지 않는 부분으로 나누어라.

                          직접 사용해보면 알겠지만 유지보수에 좋은 형태이다.

![Untitled](/images/java_Script/Untitled%208.png)


=11번 영상===========================================

[주석]

주석 ⇒ 코드의 실행에 관여하지 않는 설명문이다. 

        ⇒  // 으로 사용가능.

        ⇒ ex)  // 이 문장은 주석이다.

![Untitled](/images/java_Script/Untitled%209.png)

         ⇒ /*    */   으로도 사용 가능하다.

좋은 주석은 좋은 코드의 요인 중 하나이다.

미래의 타인이 되었을 자신을 위한 배려. 


=12번 영상===========================================

[줄바꿈과 여백]

세미 콜론 ⇒  ;  ⇒  줄이 끝났다는 표시이다.

ex)  var a = 1; alert(a);  이라 작성하면 서로 다른 줄로 인식도니다.

텝 ⇒ Tab ⇒ 들여쓰기가 된다.

                ⇒ 가독성을 높이기 위해 사용된다.

여러 줄을 드래그하고 텝하면 한 번에 들여쓰기가 적용된다.


=13번 영상===========================================

[연산자]

![Untitled](/images/java_Script/Untitled%2010.png)

a=1 에서  =(equal) 은 대입 연산자이다.

다음 영상의 내용은 대입 연산자와 다른 개념인 비교 연산자이다.


=14번 영상===========================================

[ == 과 === ]

== (equal operator).

  → 동등 연산자.

  → 두 값을 비교하여 같다면 true,  틀리다면 false를 출력한다.

![Untitled](/images/java_Script/Untitled%2011.png)

  → 문자도 비교 가능하다.

===( strict equal operator )

  → 일치 연산자.

  → 값은 물론이고, 데이터의 타입까지 같아야 true를 출력한다.

![Untitled](/images/java_Script/Untitled%2012.png)

   → == 라면 true를 출력할 것도 false를 출력하기도 한다.

   → 말 그대로 엄격한 동등 연산자이다.

   → 한 치의 오차도 용납하지 않아야 하는 중요한 코드에 사용한다.


=15번 영상===========================================

===(일치 연산자)를 사용하자.

null = 값이 없다는 뜻.

undefined = 값이 정의되지 않았다는 뜻.

NaN = 숫자가 아니라는 뜻.

alert( undefined == null)   →>>> true 가 경고창으로 출력된다.

alert( undefined === null)  →>>> false 가 경고창으로 출력된다.

[type 타입]

boolean 의 예시 →  true, false

number 의 예시 → -1, 0, 1, 2

string 의 예시 → “a”,  “b”,  “c”

null 의 예시  →  null

undefined의 예시 →  undefined

*주의 : alert( NaN === NaN ) 의 결과는 false.  NaN 에만 해당함.

타입에 관한 자세한 정보는 다음을 참조하라.

[https://opentutorials.org/module/532/4722](https://opentutorials.org/module/532/4722)

  [https://dorey.github.io/JavaScript-Equality-Table/](https://dorey.github.io/JavaScript-Equality-Table/)


=16번 영상===========================================

부정과 부등호.

!  = not =  부정을 의미한다.

alert( 1!= 2) 의 결과는 true이다. 

부등호.

>, =>, <, <=

 

=17번 영상===========================================

조건문이란.

조건문은 if로 시작한다.

**`if**(**true**){`

`alert('result : true');`

`}`

if 옆의 괄호 부분에 true가 되어야만 

중괄호 안쪽의 조건문이 실행된다.

다음을 참고하라.

[https://opentutorials.org/module/532/4724](https://opentutorials.org/module/532/4724)


=18번 영상===========================================

else, else if

else를 통해 예외를 선택해 실행할 수 있다.

**`if**(**true**){`

`alert(1);`

`} **else**` `{`

`alert(2);`

`}`

true일때는 if 부분을,

false일때는 else 부분을 실행한다.

else if는 조건문을 좀 더 풍부하게 사용할 수 있게 한다.

**`if**(**false**){`

`alert(1);`

`} **else**` **`if**(**true**){`

`alert(2);`

`} **else**` **`if**(**true**){`

`alert(3);`

`} **else**` `{`

`alert(4);`

`}`

 처음으로 true가 나온 조건문만 실행한다.

위 코드의 결과는 2이다.


=19번 영상===========================================

조건문의 응용.

prompt = 스캔문이다.

                사용자가 입력하는 정보를 받는 명령어다.

ex)  alert( prompt('당신의 나이는?')*2);

실행 시, 정보를 입력할 창이 나타난다. 

사용자가 입력하는 값에 따라 출력되는 결과가 달라진다.

ex)

`<!DOCTYPE html>`

`<**html**>`

`<**head**>`

`<**meta**` `charset="utf-8"/>`

`</**head**>`

`<**body**>`

`<**script**>`

`id = prompt('아이디를 입력해주세요.')`

`if(id=='egoing'){`

`alert('아이디가 일치 합니다.')`

`} else {`

`alert('아이디가 일치하지 않습니다.')`

`}`

`</**script**>`

`</**body**>`

`</**html**>`

prompt의 입력창에서

입력하는 아이디가 정해진것과 같아야만

‘아이디가 일치 합니다.’ 라는 문구가 출력됩니다.


=20번 영상===========================================

논리연산자.

& = 엔퍼센트. 라고 읽는다.

&& = AND 

       = 모두 true 일때만 조건문 실행.

ex)  

**`if**(**true**` `&& **true**){`

`alert(1);`

`}`

|| = or

ex)  하나만 true 여도 조건문 실행.

**`if**(**true**` `|| **true**){`

`alert(1);`

`}`


=21번 영상===========================================

boolean의 대체재.

0 = false

0이 아닌 값 = true

다음을 참고하라.

[https://opentutorials.org/module/532/4724](https://opentutorials.org/module/532/4724)


=22번 영상===========================================

반복문.

반복분 = loop = iterator

[https://opentutorials.org/module/532/4728](https://opentutorials.org/module/532/4728)

while 사용법.

`while (조건){`

`반복해서 실행할 코드`

`}`

조건이 true인한 계속해서 코드가 실행된다.

false가 된다면 코드의 반복이 종료된다.

[명령어]

document.write = 문구 출력

<br /> = 개행 

![Untitled](/images/java_Script/Untitled%2013.png)

![Untitled](/images/java_Script/Untitled%2014.png)


=23번 영상===========================================

반복조건.

다음과 같이 조건을 설정.

![Untitled](/images/java_Script/Untitled%2015.png)

i가 0~9일 때는 반복이 실행되고

i 가 10이 되면 false가 되어 반복이 중지된다.

결과적으로 Coding everybody가 10번 출력된다.


=24번 영상===========================================

for문.

while보다 편리하다. 

3가지 조건이 한 줄에 들어가기 때문.

for는 다음과 같이 사용한다.

`for(초기화; 반복조건; 반복이 될 때마다 실행되는 코드){`

`반복해서 실행될 코드`

`}`

ex) 이전 영상의 코드와 같은 결과를 낸다.

![Untitled](/images/java_Script/Untitled%2016.png)

i++  →>  다음 라인부터 i=i+1

++i  →>  현재 라인부터 i=i+1  


=25번 영상===========================================

반복문의 효용.

조건에 따라 무수한 반복조건을 실행 가능.

![Untitled](/images/java_Script/Untitled%2017.png)


=26번 영상===========================================

반복문의 제어.

break = 반복문을 종료.

continue = 현재 반복을 중지하고 다시 반복을 실행.


=27번 영상===========================================

반복문의 중첩.

다음과 같이 반복문 안에 반복문을 사용.

![Untitled](/images/java_Script/Untitled%2018.png)

결과적으로 Coding everybody 0 ~ Coding everybody 99가 출력된다.

[디버그]

도구 → 개발자 도구 →  Source → F5키.

 

![Untitled](/images/java_Script/Untitled%2019.png)

for가 있는 8번 라인을 클릭.

breakpoints에 for의 정보가 표시된다.

이 상태에서 F5키를 입력 →  Pause in debugger 뜨면서 회색 화면 출력됨.

코드 실행이 8번까지 와서 멈춘 것이다.

해당 상태에서 아래쪽의 코드제어 도구들을 사용 가능하다.

![Untitled](/images/java_Script/Untitled%2020.png)

첫 번째 도구 = 코드 재실행.

두 번째 도구 = 

세 번째 도구 = 다음 라인 실행

네 번째 도구 = 이전 라인 실행

코드제어 도구 옆 같에서 다음과 같이 표시 가능.

![Untitled](/images/java_Script/Untitled%2021.png)

이 상태에서 벗어나기 =  8번 breakpoint를 클릭하고 첫 번째 도구를 누른다.


=28번 영상===========================================

함수.

재사용성이 높은 기능.

다음과 같이 사용한다.

**`function`** `함수명( [인자...[,인자]] ){`

`코드`

`**return**` `반환값`

`}`

ex) numbering이란 함수를 정의.

![Untitled](/images/java_Script/Untitled%2022.png)

변수와 달리 옆에 괄호가 있어야 한다.

그래야 변수가 아닌 함수로 인식된다.

자세한 내용은 다음을 참고.

[https://opentutorials.org/module/532/4729](https://opentutorials.org/module/532/4729)


=29번 영상===========================================

함수의 효용.

한 번 정의한 함수는 재사용성,

유지보수의 용이성, 가독성이 띄어나다.


=30번 영상===========================================

입력과 출력.

출력 = return

return = 출력과 동시에 함수를 종료시킨다.

**`function`** `get_member1(){`

`**return**` `'egoing';`

`}`

**`function`** `get_member2(){`

`**return**` `'k8805';`

`}`

`alert(get_member1());`

`alert(get_member2());`

출력 예시 = return에 의하여 alert가 egoing과 k8805를 출력된다.


=31번 영상===========================================

입력과 출력.

매개변수(parameter) = 입력받는 변수  

인자(argument) = 함수로 유입되는 입력 값

![Untitled](/images/java_Script/Untitled%2023.png)

입력 예시 = alert의 실행에서 함수의 괄호에 든 값이 변수 arg에 입력된다.


=32번 영상===========================================

다양한 정의 방법.

정의 방법 예시.

![Untitled](/images/java_Script/Untitled%2024.png)

위 코드는 아래 코드와 같다고 볼 수 있다.

![Untitled](/images/java_Script/Untitled%2025.png)

[익명함수]

다음과 같이 함수 전체를 괄호로 덮는 것이다.

함수정의와 동시에 ;옆의 ()에 의해 함수 호출이 발동.

즉, 함수 정의와 함수 호출이 동시에 되어 일회성으로 사용되는 함수가 된다.

![Untitled](/images/java_Script/Untitled%2026.png)


=33번 영상===========================================

배열의 문법.

배열(array) = 연관된 데이터를 모아 관리하기 위한 데이터 타입.

                   = 변수가 하나의 데이터를 저장한다면 배열은 다수를 관리.

ex)  **`var**member = ['egoing', 'k8805', 'sorialgi']`

- 위 코드의 member는 3개의 원소를 가진 배열이다.
- 배열에 담긴 원소는 0번, 1번, 2번....순서로 저장된다.
- 이 원소의 위치를 색인(index) 라고 한다.

 

=34번 영상===========================================

배열의 효용.

함수는 여러개의 입력이 가능한 것에 비해 출력은 하나만 가능하다.

그러나 배열을 이용해 return을 하면 여러 개의 출력이 가능해진다.

 ex) 

**`function`** `get_members(){`

`**return**` `['egoing', 'k8805', 'sorialgi'];`

`}`


=35번 영상===========================================

배열과 반복문의 조우.

toUpperCase(); = 대문자로 바꿔주는 내장함수.

                         = 다음과 같이 사용 가능하다.

![Untitled](/images/java_Script/Untitled%2027.png)

위 함수를 이용한 예시이다.

**`function`** `get_members(){`

`**return**` `['egoing', 'k8805', 'sorialgi'];`

`}`

**`var`** `members = get_members();`

`document.write(members[0]);`

`document.write(members[1]);`

`document.write(members[2]);`

이 코드를 반복문을 통해 재구현하면 다음과 같다.

![Untitled](/images/java_Script/Untitled%2028.png)

결과 : 배열의 원소들이 대문자로 출력된다.


=36번 영상===========================================

데이터의 추가.

push() = 배열에 원소 추가.

concat() = 배열에 복수의 원소 추가.

ex)

![Untitled](/images/java_Script/Untitled%2029.png)

unshift() = 배열의 0번 자리에 원소 추가

ex)

![Untitled](/images/java_Script/Untitled%2030.png)

splice() = 배열의 중간에 추가

ex) splice(1,0,’d’) → 1번 자리에 원소를 0개 삭제하고 ‘d’를 추가

![Untitled](/images/java_Script/Untitled%2031.png)


=37번 영상===========================================

제거와 정렬.

shift() = 배열의 0번 자리의 원소를 제거

ex)

![Untitled](/images/java_Script/Untitled%2032.png)

pop() = 배열의 끝의 원소를 제거

ex)

![Untitled](/images/java_Script/Untitled%2033.png)

sort() = 배열의 원소를 정렬

ex)

![Untitled](/images/java_Script/Untitled%2034.png)

reverse() = 배열의 원소를 거꾸로 정렬

ex)

![Untitled](/images/java_Script/Untitled%2035.png)


=38번 영상===========================================

객체.

배열은 아이템에 대한 식별자로 숫자를 사용했다.

객체를 사용한다면 문자를 인덱스로 사용할 수 있다.

다음은 객체를 만드는 법이다.

 **`var**grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};`

위와 같이 인덱스와 값이 쌍을 이룬다. (key-value 쌍)

다음과 같이 객체를 만들 수도 있다.

**`var`** `grades = {};`

`grades['egoing'] = 10;`

`grades['k8805'] = 6;`

`grades['sorialgi'] = 80;`

만들어진 객체는 다음과 같이 이용할 수 있다.

![Untitled](/images/java_Script/Untitled%2036.png)

[ ]를 사용하면 다음같이 사용 가능.

![Untitled](/images/java_Script/Untitled%2037.png)


=39번 영상===========================================

객체와 반복문의 조우.

반복문에서 다음과 같이 사용.

참고로, 태크인 <ul> ~ </ul>은 리스트를 뜻함.

                         <li> ~ </li> 는 document.write로 작성한 부분이라 한다.

                          ( li = list 의 약자) 

![Untitled](/images/java_Script/Untitled%2038.png)

for문에 의해 반복마다 변수 name에 배열 grades의 원소가 입력된다.

결과는 다음과 같다.

![Untitled](/images/java_Script/Untitled%2039.png)

다음과 같은 활용도 가능하다.

![Untitled](/images/java_Script/Untitled%2040.png)


=40번 영상===========================================

객체지향 프로그래밍.

배열 안에 함수를 정의하는 법.

![Untitled](/images/java_Script/Untitled%2041.png)

결과는 ‘Hello world’

또 다른 예시.

![Untitled](/images/java_Script/Untitled%2042.png)

결과는 egoing 10

      k8805 8

sorialgi 80


=41번 영상===========================================

모듈.

*모듈

 - 부품. 작고 단순한 것에서 크고 복잡한 것으로 진화한다.

 - 코드의 재활용성을 높이고, 유지보수를 쉽게 한다.

*묘듈의 장점

 - 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 활용 가능.

 - 코드 수정 시에 필요한 로직을 빠르게 찾을 수 있다.

 - 필요한 로직만을 로드해서 메모리의 낭비를 줄일 수 있다.


=42번 영상===========================================

모듈화.

main.html 파일 생성.

[https://opentutorials.org/module/532/4750](https://opentutorials.org/module/532/4750)

링크의 코드 복사 붙여넣기.

![Untitled](/images/java_Script/Untitled%2043.png)

src = “greeting.js” →>> 함수를 정의한 후에 호출하는 것과 같은 효과.

greeting.js 파일 생성.

파일에 함수 부분의 코드를 작성. 

main.html의 함수 부분은 지운다.

![Untitled](/images/java_Script/Untitled%2044.png)

 

두 파일을 작성 완료했으면 main에서 실행.

![Untitled](/images/java_Script/Untitled%2045.png)

ctrl + o 를 통해 main.html을 열고 코드를 실행한다.

greeting.js이 호출되어 main에서 실행되는 결과가 나온다.


=43번 영상===========================================

Node.js의 모듈화.

다른 환경에서의 모듈은 다루는 방법이 다름.

이 영상에선 오직 그것만 인지하면 됨.


=44번 영상===========================================

라이브러리란?

[라이브러리]

- 모듈과 비슷한 개념.
- 자주 사용되는 로직을 재사용하기 편리하도록 정리한 코드들의 집합.
- 유명 라이브러리로는 jQuery 가 있다.


=45번 영상===========================================

라이브러리의 사용.

jQuery 사용법.

- jQuery에서 파일을 다운로드 받는다.
- API documentation을 보고 사용법을 숙지한다.
- 두 가지를 이용하여 라이브러리를 사용.

실제 사용법.

1. 구글에서 jquery를 검색.
2. jquery에서 파일을 다운받는다.  [https://code.jquery.com/jquery-3.6.0.js](https://code.jquery.com/jquery-3.6.0.js)
3. 다운받으면 나타나는 페이지를 전체 복사(Ctrl+A)
4. jquery.js파일을 생성하고 복사한 내용을 붙여넣기.
5. script 부분에 src=”jquery.js”를 작성하여 실행하면 jquery를 사용할 수 있다. 

![Untitled](/images/java_Script/Untitled%2046.png)

jquery 코드 작성

- jquery의 코드는 $로 시작한다.

다음은 <li>~</li> 에 있는 empty를 바꾸는 실행문이다.

![Untitled](/images/java_Script/Untitled%2047.png)

excute라는 버튼을 생성.

excute 버튼을 click시에 발동하는 함수 정의.

함수 내용은 li에 있는 텍스트를 coding everybody로 변경.

따라서 다음 결과가 나온다.

![Untitled](/images/java_Script/Untitled%2048.png)

버튼을 누르면 다음과 같이 텍스트가 변경된다.

![Untitled](/images/java_Script/Untitled%2049.png)


=46번 영상===========================================

JavaScript-UI,API 그리고 문서

[https://opentutorials.org/module/532/6533](https://opentutorials.org/module/532/6533)


=47번 영상===========================================

UI와 API.

UI = User Interface

API = Application Programming Interface

UI는 코드를 모르는 사용자도 쉽게 다룰 수 있도록 해주는 편의성 중심 기술.

사용자의 의도를 손쉽게 pc에 전달하여 조작 난이도를 낮춰준다.

internet explore 의 주소창에 다음 명령어를 입력.

javascript.alert("Hello world");

경고창으로 Hello world가 출력된다.

이 경고창을 내가 만들었는지 시스템이 만들었는지는 애매하다.

하지만, 이 경고창의 ‘확인’에 커서를 갖다대면 색이 변하는 것이나

경고창이 뜨면서 나오는 경고음, 경고창의 위치 등은 확실하게

내가 만들었다고 할 수 없다.

이런 것들이 모두 API라고 할 수 있다. 

물론 alert등의 명령어도 이에 포함된다.

정리하다면, 사용자는 UI를 통해 시스템을 사용하고

                    개발자는 UI와 API를 통해 시스템을 다룬다.

![Untitled](/images/java_Script/Untitled%2050.png)


=48번 영상===========================================

문서 보는 법.

프로그래밍을 공부하기 위한 자료 - 레퍼런스, 튜토리얼

튜토리얼 = 언어의 문법을 설명.

레퍼런스 = 명령어의 사전.

자바스크립트 API는 크게 자바스크립트 자체의 API와 

자바스크립트가 동작하는 호스트 환경의 API로 구분된다.

자바스크립트 API 문서 예시

- ECMA script (표준문서)
- 자바스트립트 사전 : [https://opentutorials.org/course/50](https://opentutorials.org/course/50)
- 자바스크립트 레퍼런스 (MDN)
- jscript 레퍼런스 (MSDN)


=49번 영상===========================================

정규표현식.

정규표현식은 문자열에서 특정한 문자를 찾아내는 도구다.

더 자세한 내용을 알고 싶다면 다음을 참고.

[https://opentutorials.org/module/532/6580](https://opentutorials.org/module/532/6580)

[https://opentutorials.org/course/909/5142](https://opentutorials.org/course/909/5142) 


=50번 영상===========================================

정규표현식 : 패턴만들기

정규표현식 사용은 두가지 단계로 이루어짐.

[ 1단계 ] 컴파일 ⇒ 패턴을 찾는 것.

var str = “a”;  즉, a 라는 텍스트를 찾아내는 정규표현식을 만들어보자.

  방법 1) 정규표현식 리터럴

**`var**pattern = /a/`

  방법 2) 정규표현식 객체 생성자

`var pattern = new RegExp('a');`

[ 2단계 ]  실행 ⇒ 찾은 패턴을 구체화하는 것.


=51번 영상===========================================

정규표현식 : RegExp 객체의 정규 표현식

정규표현식을 컴파일해서 객체를 만들었다면

이제 문자열에서 원하는 문자를 찾아내야 한다.

RegExp.exec()

다음과 같이 사용한다.

![Untitled](/images/java_Script/Untitled%2051.png)

찾으려는 문자를 변수 pattern에 정의한 다음,

exec() 의 괄호에 아무 문자열이나 채워넣는다.

pattern.exec()를 실행하면 문자열중에서 pattern에 해당하는 문자를 찾아낸다.

RegExp.test()

다음과 같이 사용한다.

![Untitled](/images/java_Script/Untitled%2052.png)

exec()와 같이 사용한다.

다만 결과는 boolean 값으로 출력된다.

찾는 문자가 있다면 true, 없다면 false.


=52번 영상===========================================

 정규표현식 : String 객체의 정규 표현식

string.match()

다음과 같이 사용한다.

![Untitled](/images/java_Script/Untitled%2053.png)

exec()와 비슷하다.

string.replace()

다음과 같이 사용한다.

![Untitled](/images/java_Script/Untitled%2054.png)

str에 입력된 문자열에서

replace()에 입력한 pattern을 찾은 후에

( )안의 인자로 대체한다.


=53번 영상===========================================

정규표현식 : 옵션

/i  ⇒  소문자 대문자 모두 찾는 옵션.

     =  a를 지정했음에도 “A”를 찾아 출력함. 

![Untitled](/images/java_Script/Untitled%2055.png)

/g  ⇒ 같은 문자가 여러 개 나와도 모두 찾는다. (글로벌)

![Untitled](/images/java_Script/Untitled%2056.png)


=54번 영상===========================================

정규표현식 : 캡처

괄호안의 패턴은 마치 변수처럼 재사용할 수 있다.

이 때 기호 $를 사용하는데 아래 코드는 coding과 everybody의 순서를 역전시킨다.

**`var`** `pattern = /(\w+)\s(\w+)/;`

**`var`** `str = "coding everybody";`

**`var`** `result = str.replace(pattern, "$2, $1");`

`console.log(result);`

(\w+)\s(\w+)  ⇒  ‘문자+(공백)+문자’ 를 표현한 식이다.

이 식을 이용하여 다음 링크들을 살펴보자. 

[https://regexper.com/](https://regexper.com/)

- 정규표현식 시각화 페이지
- 입력한 식을 시각화하여 보여준다.

[https://regexr.com/](https://regexr.com/)

- 정규표현식 빌더
- 텍스트박스에 식을 입력한다.
- 아래의 박스에 여러 단어를 입력한다.
- 텍스트박스의 식과 일치하는 아래 박스의 단어는 파랗게 빛난다.


=55번 영상===========================================

정규표현식 : 치환

다음 코드는 본문 중의 URL을 링크 html 태그로 교체한다.

**`var`** `urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim;`

**`var`** `content = '생활코딩 : [http://opentutorials.org/course/1](http://opentutorials.org/course/1) 입니다. 네이버 : [http://naver.com](http://naver.com/) 입니다. ';`

**`var`** `result = content.replace(urlPattern, **function**(url){`

`**return**` `'<a href="'+url+'">'+url+'</a>';`

`});`

`console.log(result);`


=56번 영상===========================================

유효범위 : 전역변수화 지역변수

[https://opentutorials.org/module/532/6495](https://opentutorials.org/module/532/6495)

유효범위(Scope)는 변수의 수명을 위미.

**`var`** `vscope = 'global';`

**`function`** `fscope(){`

   `var vsope = 'local';`

`alert(vscope);`

`}`

`fscope();`

함수 내에 선언된 vscope에 의해 local이 출력된다.

만약, 함수 내의 vscope이 없다면 함수 밖의 global이 출력된다.

함수 내에서 var로 변수 정의한 것은 ‘로컬(지역)변수’가 된다.

만약, var을 붙이지 않는다면 전역변수가 된다.

![Untitled](/images/java_Script/Untitled%2057.png)

따라서, 위 코드에서 함수 내의 vscope=’local’에 의해

맽 윗줄의 var vscope 의 내용물은 ‘global’에서 ‘local’이 된다.

단, 같은 함수 내에 이미 같은 변수가 지역변수로 존재한다면

var이 안 붙어있어도 지역변수로 취급된다.


=57번 영상===========================================

유효범위 : 유효범위와 효용

아래 두개의 예제는 변수 i를 지역변수로 사용했을 때와 전역변수로 사용했을 때의 차이점을 보여준다. 전역변수는 각기 다른 로직에서 사용하는 같은 이름의 변수값을 변경시켜서 의도하지 않은 문제를 발생시킨다.

**`function`** `a (){`

`**var**` `i = 0;`

`}`

**`for**(**var**` `i = 0; i < 5; i++){`

`a();`

`document.write(i);`

`}`

결과 : 01234

**`function`** `a (){`

`i = 0;`

`}`

**`for**(i = 0; i < 5; i++){`

`a();`

`document.write(i);`

`}`

결과 : 무한반복


=58번 영상===========================================

유효범위 : 전역변수를 사용하는 법

불가피하게 전역변수를 사용해야 하는 경우는 하나의 객체를 전역변수로 만들고 객체의 속성으로 변수를 관리하는 방법을 사용한다. 

다음은 전역변수 하나를 선언하고

나머지 변수는 전역변수의 소속변수로 둔 것이다.

따라서 다른 코드의 이름이 같은 변수와 충돌할 가능성을 줄일 수 있다.

var `MYAPP = {}`

`MYAPP.calculator = {`

`'left'` `: **null**,`

`'right'` `: **null**`

`}`

`MYAPP.coordinate = {`

`'left'` `: **null**,`

`'right'` `: **null**`

`}`

`MYAPP.calculator.left = 10;`

`MYAPP.calculator.right = 20;`

**`function`** `sum(){`

`**return**` `MYAPP.calculator.left + MYAPP.calculator.right;`

`}`

`document.write(sum());`

결과 : 10+20=30


=59번 영상===========================================

유효범위 : 유효범위의 대상

자바스크립트는 함수에 대한 유효범위만을 제공한다. 많은 언어들이 블록(대체로 {,})에 대한 유효범위를 제공하는 것과 다른 점이다. 아래 예제의 결과는 coding everybody이다.

**`for**(**var**` `i = 0; i < 1; i++){`

`**var**` `name = 'coding everybody';`

`}`

`alert(name);`

자바에서는 아래의 코드는 허용되지 않는다. name은 지역변수로 for 문 안에서 선언 되었는데 이를 for문 밖에서 호출하고 있기 때문이다

**`for**(int i = 0; i < 10; i++){`

`String name = "egoing";`

`}`

`System.out.println(name);`


=60번 영상===========================================

유효범위 : 정적 유효 범위

자바스크립트는 함수가 선언된 시점에서의 유효범위를 갖는다.

이러한 유효범위의 방식을 정적 유효범위(static scoping),

혹은 렉시컬(lexical scoping)이라고 한다.

**`var`** `i = 5;`

**`function`** `a(){`

`**var**` `i = 10;`

`b();`

`}`

**`function`** `b(){`

`document.write(i);`

`}`

`a();`

결과 : 5

[정적 유효범위 개념]

사용될 때가 아니라,

정의될 때를 기준으로 하기 때문에 결과는 5이다.

 

=61번 영상===========================================

값으로서의 함수와 콜백 : 함수의 용도1 

[https://opentutorials.org/module/532/6508](https://opentutorials.org/module/532/6508)

JavaScript에서는 함수도 객체다.

 다시 말해서 일종의 값이다. 

거의 모든 언어가 함수를 가지고 있다. 

JavaScript의 함수가 다른 언어의 함수와 다른 점은

함수 자체  값이 될 수 있다는 점이다.

**`function**a(){}`

위 코드에서 함수 a는 변수 a에 담겨진 값이다. 

또한 함수는 객체의 값으로 포함될 수 있다.

이렇게 객체의 속성 값으로 담겨진 함수를 메소드(method)라고 부른다.

`a = {`

`b:**function**(){`

`}`

`};`

위 코드에서 a안에 담긴 b라는 속성(property)이 있다고 볼 수 있으며,

중괄호 안의 함수 function은 메소드(method)이다.

객체 내에서 정의된 함수는 메소드이므로

a 라는 객체 안에서 정의된 함수 function은 메소드이다.

함수는 값이기 때문에 다른 함수의 인자로 전달 될수도 있다.

다음과 같이 사용 가능.

**`function`** `cal(func, num){`

`**return**` `func(num)`

`}`

**`function`** `increase(num){`

`**return**` `num+1`

`}`

**`function`** `decrease(num){`

`**return**` `num-1`

`}`

`alert(cal(increase, 1));`

`alert(cal(decrease, 1));`


=62번 영상===========================================

값으로서의 함수와 콜백 : 함수의 용도2

함수는 함수의 리턴 값으로도 사용할 수 있다.

**`function`** `cal(mode){`

`**var**` `funcs = {`

`'plus'` `: **function**(left, right){**return**` `left + right},`

`'minus'` `: **function**(left, right){**return**` `left - right}`

`}`

`**return**` `funcs[mode];`

`}`

`alert(cal('plus')(2,1));`

`alert(cal('minus')(2,1));`

결과 : 3, 1

 배열의 값으로도 사용할 수 있다.

**`var`** `process = [`

`**function**(input){ **return**` `input + 10;},`

`**function**(input){ **return**` `input * input;},`

`**function**(input){ **return**` `input / 2;}`

`];`

**`var`** `input = 1;`

**`for**(**var**` `i = 0; i < process.length; i++){`

`input = process[i](input);`

`}`

`alert(input);`

for문에 의해 배열에 담긴 함수가 차례로 호출.

input=1 → input+10=11 → input*input=121 → input/2=60.5

결과 : 60.5


=63번 영상===========================================

값으로서 함수와 콜백 : 콜백

sort() 는 내장 메소드이다.

![Untitled](/images/java_Script/Untitled%2058.png)

위 코드를 실행하면 sort()에 따라 배열이 정렬된다.

하지만 우리가 원하는 배열이 되지 않는다.

![Untitled](/images/java_Script/Untitled%2059.png)

sort()는 앞에 온 문자로 순서를 판단하는 듯 하다.

크기 순서로 배열하려면 array()를 사용해야 한다.

자바스크립트 사전에서 array의 원리를 파악하고 코딩한 결과이다.

결과로 배열이 제대로 정렬되어 출력된다.

![Untitled](/images/java_Script/Untitled%2060.png)

값으로 전달된 함수는 호출될 수 있기 때문에

이를 이용하면 함수의 동작을 완전히 바꿀 수 있다.

이것을 ‘콜백’이라고 하며,

이것이 가능한 것은 자바스크립트에서

함수가 값으로 취급되기 때문이다.


=64번 영상===========================================

값으로서 함수와 콜백 : 비동기 콜백

콜백은 ‘비동기처리’에서도 유용하게 사용된다.

시간이 오래걸리는 작업이 있을 때 

이 작업이 완료된 후에 처리해야 할 일을 콜백으로 지정하면

해당 작업이 끝났을 때 미리 등록한 작업을 실행하도록 할 수 있다.

to-do와 비슷하다.

동기화는 비동기화의 반대되는 개념이다.

비동기 처리의 예시로는 Ajax가 있다.

Ajax = asynchronous java script and XML

               ( 비동기 )


=65번 영상===========================================

클로저 : 외부함수와 내부함수

[https://opentutorials.org/module/532/6544](https://opentutorials.org/module/532/6544)

클로저(closure)는 내부함수가

외부함수의 맥락(context)에

접근할 수 있는 것을 가르킨다.

**`function`** `outter(){`

`**function**` `inner(){`

`**var**` `title = 'coding everybody';`

`alert(title);`

`}`

`inner();`

`}`

`outter();`

위 코드에서 inner()는 내부함수,

outer()는 외부함수이다.

내부함수는 외부함수의 지역변수에 접근할 수 있다.

**`function`** `outter(){`

`**var**` `title = 'coding everybody';`

`**function**` `inner(){`

`alert(title);`

`}`

`inner();`

`}`

`outter();`

결과 : coding everybody

이 결과는 inner() 외부함수의 지역변수인 var title에

접근할 수 있음을 알려준다.


=66번 영상===========================================

클로저 : 클로저란

클로저(closure)는 내부함수와 밀접한 관계를 가지고 있는 주제다.

내부함수는 외부함수의 지역변수에 접근 할 수 있는데

외부함수의 실행이 끝나서 외부함수가 소멸된 이후에도

내부함수가 외부함수의 변수에 접근 할 수 있다.

이러한 메커니즘을 클로저라고 한다.

**`function`** `outter(){`

`**var**` `title = 'coding everybody';`

`**return**` **`function**(){`

`alert(title);`

`}`

`}`

`inner = outter();`

`inner();`

결과 : coding everybody


=67번 영상===========================================

클로저 : private variable

다음은 클로저를 이용해 영화의 제목을 저장하고 있는 객체를 정의하고 있다.

**`function`** `factory_movie(title){`

`**return**` `{`

`get_title : **function**` `(){`

`**return**` `title;`

`},`

`set_title : **function**(_title){`

`title = _title`

`}`

`}`

`}`

`ghost = factory_movie('Ghost in the shell');`

`matrix = factory_movie('Matrix');`

`alert(ghost.get_title());`  → Ghost in the shell

`alert(matrix.get_title());`  → Matrix

`ghost.set_title('공각기동대');`

`alert(ghost.get_title());`   → 공각기동대

`alert(matrix.get_title());`  → Matrix

각각 자신이 실행된 시점에서의 title값에 접근한다.

private variable = 비밀변수.

private variable의 개념으로 title이란 변수를 안전하게 저장한 것이다. 


=68번 영상===========================================

클로저 :  클로저의 응용

클로저 사용 시 주의점.

**`var`** `arr = []`

**`for**(**var**` `i = 0; i < 5; i++){`

`arr[i] = **function**(){`

`**return**` `i;`

`}`

`}`

**`for**(**var**` `index **in**` `arr) {`

`console.log(arr[index]());`

`}`

결과 : 5 5 5 5 5

- 설명이 이해가 되지 않았다. 다시 보자.


=69번 영상===========================================

arguments : arguments란?

arguments는 배열과 유사하지만, 배열은 아니다. 

실제로는 arguments 객체의 인스턴스다.

**`function`** `sum(){`

`**var**` `i, _sum = 0;`

`**for**(i = 0; i < arguments.length; i++){`

`document.write(i+' : '+arguments[i]+'<br />');`

`_sum += arguments[i];`

`}`

`**return**` `_sum;`

`}`

`document.write('result : '` `+ sum(1,2,3,4));`

arguments의 자체적인 기능으로 인해

sum() 안에 몇 개의 인자가 담겨있는지 파악이 가능하다.

그렇기에 위 코드 실행 시, argument.length = 4 가 된다.


=70번 영상===========================================

arguments : function length

매개변수와 관련된 두가지 수가 있다.

하나는 함수.length, 다른 하나는 arguments.length이다.

arguments.length는 함수로 전달된 실제 인자의 수를 의미하고, 

함수.length는 함수에 정의된 인자의 수를 의미한다.

**`function`** `zero(){`

`console.log(`

`'zero.length', zero.length,`

`'arguments', arguments.length`

`);`

`}`

**`function`** `one(arg1){`

`console.log(`

`'one.length', one.length,`

`'arguments', arguments.length`

`);`

`}`

**`function`** `two(arg1, arg2){`

`console.log(`

`'two.length', two.length,`

`'arguments', arguments.length`

`);`

`}`

`zero(); // zero.length 0 arguments 0`

`one('val1', 'val2');  // one.length 1 arguments 2`

`two('val1');  // two.length 2 arguments 1`


=71번 영상===========================================

함수의 호출 : apply 소개

[https://opentutorials.org/module/532/6550](https://opentutorials.org/module/532/6550)

함수를 호출하는 가장 기본적인 방법이다

**`function`** `func(){`

`}`

`func();`

함수 func는 Function이라는 객체의 인스턴스다.

따라서 func는 객체 Function이 가지고 있는 메소드들을 상속하고 있다. 

해당 영상에서 이야기하려는 메소드는 Function.apply과 Function.call이다

**`function`** `sum(arg1, arg2){`

`**return**` `arg1+arg2;`

`}`

`alert(sum.apply(**null**, [1,2]))`   → 3

함수 sum은 Function 객체의 인스턴스다.

그렇기 때문에 객체 Function 의 메소드 apply를 호출 할 수 있다.

apply 메소드는 두개의 인자를 가질 수 있는데,

첫번째 인자는 함수(sum)가 실행될 맥락이다.

두번째 인자는 배열인데, 

이 배열의 담겨있는 원소가 함수(sum)의 인자로 순차적으로 대입된다.


=72번 영상===========================================

함수의 호출 : apply의 사용

this는 호출할 때 결정된다.

`o1 = {val1:1, val2:2, val3:3}`

`o2 = {v1:10, v2:50, v3:100, v4:25}`

**`function`** `sum(){`

`**var**` `_sum = 0;`

`**for**(name **in**` **`this**){`   → 코드 실행 시, var this = o1 이 된다.

`_sum += **this**[name];`

`}`

`**return**` `_sum;`

`}`

`alert(sum.apply(o1)) // 6`

`alert(sum.apply(o2)) // 185`


=73번 영상===========================================

객체지향프로그래밍 : 오리엔테이션

[https://opentutorials.org/module/532/6553](https://opentutorials.org/module/532/6553)

객체지향 프로그래밍(Object-Oriented Programming)

객체는 틀이다.

붕어빵을  만드는 틀과 같이 정해진 형태가 있으며,

틀에서 만들어진 붕어빵과 같이

객체 역시 자신과 같은 형태를 계속해서 찍어낼 수 있다.


=74번 영상===========================================

객체지향프로그래밍 : 추상화

좋은 객체를 만들기 위해서는 설계가 중요하다.

좋은 설계는 현실을 잘 반영해야 한다.

현실은 복잡하지만 그 복잡함 전체가 필요한 것은 아니다.

지하철 노선도를 떠올리면 간단하다.

노선도마냥 알기 쉽게하는 과정을  ‘추상화(abstract)’라고 한다.


=75번 영상===========================================

객체지향프로그래밍 : 부품화

객체 지향은 ‘부품화’의 정점이라고 할 수 있다.

배운 것 중에서 부품화의 특성을 보여줄 수 있는 기능을 생각해보자.

메소드는 부품화의 예라고 할 수 있다.

메소드를 사용하는 기본 취지는 

연관되어 있는 로직들을 결합해서 메소드라는 완제품을 만드는 것이다.

그리고 이 메소드들을 부품으로 해서 

하나의 완제품인 독립된 프로그램을 만드는 것이다.

메소드를 사용하면 코드의 양을 극적으로 줄일 수 있고, 

메소드 별로 기능이 분류되어 있기 때문에

필요한 코드를 찾기도 쉽고 문제의 진단도 빨라진다.


=76번 영상===========================================

생성자와 new : 소개

[https://opentutorials.org/module/532/6570](https://opentutorials.org/module/532/6570)

자바스크립트 = prototype-based programming.

자바스크립트의 객체 지향 사용법을 알아보자.

다른 언어와 사용법이 다르다고 하니 주의.


=77번 영상===========================================

생성자와 new : 객체생성

객체란 서로 연관된 변수와 함수를 그룹핑한 그릇이라고 할 수 있다. 

객체 내의 변수를 프로퍼티(property) 함수를 메소드(method)라고 부른다. 

객체를 만들어보자.

**`var`** `person = {}`

`person.name = 'egoing';`

`person.introduce = **function**(){`

`**return**` `'My name is '+**this**.name;`

`}`

`document.write(person.introduce());`  → My name is egoing

이런 형태로 코드를 작성하다 보면 중복이 발생할 수 있다.

그것을 막기 위해서 생성자를 사용해야 한다. 


=78번 영상===========================================

생성자와 new : 생성자와 new

생성자(constructor)는 객체를 만드는 역할을 하는 함수다.

자바스크립트에서 함수는 재사용 가능한 로직의 묶음이 아니라 

객체를 만드는 창조자라고 할 수 있다.

생성자는 new를 사용한다.

**`function`** `Person(){}`

`var p = new Person();`

`p.name = 'egoing';`

`p.introduce = **function**(){`

`**return**` `'My name is '+this.name;`

`}`

`document.write(p.introduce());`

자바스크립트에서 생성자는 소속이 없다. 

생성자는 함수일 뿐이다.

자바스크립트에선 클래스라는 것이 없다.

다음은 생성자를 이용해 재사용성이 높은 코드를 작성한 것이다.

**`function`** `Person(name){`

`**this**.name = name;`

`**this**.introduce = **function**(){`

`**return**` `'My name is '+**this**.name;`

`}`

`}`

**`var`** `p1 = **new**` `Person('egoing');`

`document.write(p1.introduce()+"<br />");`

**`var`** `p2 = **new**` `Person('leezche');`

`document.write(p2.introduce());`

생성자 내에서 이 객체의 프로퍼티를 정의하고 있다. 

이러한 작업을 초기화(initalize)라고 한다. 

이를 통해서 코드의 재사용성이 대폭 높아졌다.

코드를 통해서 알 수 있듯이 생성자 함수는

일반함수와 구분하기 위해서 첫글자를 대문자로 표시한다.


=79번 영상===========================================

전역객체

[https://opentutorials.org/module/532/6577](https://opentutorials.org/module/532/6577)

전역객체(Global object)는 특수한 객체다. 

모든 객체는 이 전역객체의 프로퍼티다.

![Untitled](/images/java_Script/Untitled%2061.png)

window는 전역 객체이다.

window.func()와 func()는 같은 명령이며 window는 생략하여 사용이 가능하다.

우리는 우리도 모르게 window를 사용하고 있었다.


=80번 영상===========================================

this : 함수와 this

[https://opentutorials.org/module/532/6571](https://opentutorials.org/module/532/6571)

this는 함수 내에서 함수 호출 맥락(context)를 의미한다.

맥락이라는 것은 상황에 따라서 달라진다는 의미이다. 

즉 함수를 어떻게 호출하느냐에 따라서 

this가 가리키는 대상이 달라진다는 뜻이다.

this는 전역객체인 window와 같다.

**`function`** `func(){`

`**if**(window === **this**){`

`document.write("window === this");`

`}`

`}`

`func();`  →>> window === this


=81번 영상===========================================

this : 메소드와 this

객체의 소속인 메소드의 this는 그 객체를 가르킨다.

**`var`** `o = {`

`func : **function**(){`

`**if**(o === **this**){`

`document.write("o === this");`

`}`

`}`

`}`

`o.func();`  →>>  o === this


=82번 영상===========================================

this : 생성자와 this

아래 코드는 함수를 호출했을 때와

new를 이용해서 생성자를 호출했을 때의 차이를 보여준다.

**`var`** `funcThis = **null**;`

**`function`** `Func(){`

`funcThis = **this**;`

`}`

**`var`** `o1 = Func();`

**`if**(funcThis === window){`

`document.write('window <br />');` →>> window

`}`

**`var`** `o2 = **new**` `Func();`

**`if**(funcThis === o2){`

`document.write('o2 <br />');`  →>> o2

`}`


=83번 영상===========================================

this : 객체로서 함수

함수가 객체인 것에 대한 설명.

![Untitled](/images/java_Script/Untitled%2062.png)


=84번 영상===========================================

this : apply와 this

함수의 메소드인 apply, call을 이용하면 this의 값을 제어할 수 있다.

**`var`** `o = {}`

**`var`** `p = {}`

**`function`** `func(){`

`**switch**(**this**){`

`**case**` `o:`

`document.write('o<br />');`

`**break**;`

`**case**` `p:`

`document.write('p<br />');`

`**break**;`

`**case**` `window:`

`document.write('window<br />');` 

`**break**;`

`}`

`}`

`func();`    →>> window

`func.apply(o);`  →>> o

`func.apply(p);`  →>> p


=85번 영상===========================================

상속 : 상속이란?

[https://opentutorials.org/module/532/6572](https://opentutorials.org/module/532/6572)

객체는 연관된 로직들로 이루어진 작은 프로그램이라고 할 수 있다. 

상속은 객체의 로직을 그대로 물려 받는

또 다른 객체를 만들 수 있는 기능을 의미한다. 

단순히 물려받는 것이라면 의미가 없을 것이다. 

기존의 로직을 수정하고 변경해서 파생된 새로운 객체를 만들 수 있게 해준다.

![Untitled](/images/java_Script/Untitled%2063.png)


=86번 영상===========================================

상속 : 상속의 사용방법

**`function`** `Person(name){`  // 생성자

`**this**.name = name;`

`}`

`Person.prototype.name=**null**;`

`Person.prototype.introduce = **function**(){`

`**return**` `'My name is '+**this**.name;`

`}`

**`function`** `Programmer(name){`  // 객체화

`**this**.name = name;`

`}`

`Programmer.prototype = **new**` `Person();` // 상속

**`var`** `p1 = **new**` `Programmer('egoing');`

`document.write(p1.introduce()+"<br />");` // 상속으로 introduce 사용 가능


=87번 영상===========================================

상속 : 기능의 추가

다음 코드에서 Programmer는 Person의 기능을 가지고 있으면서

Person이 가지고 있지 않은 기능인 메소드 coding을 가지고 있다.

**`function`** `Person(name){`

`**this**.name = name;`

`}`

`Person.prototype.name=**null**;`

`Person.prototype.introduce = **function**(){`

`**return**` `'My name is '+**this**.name;`

`}`

**`function`** `Programmer(name){`

`**this**.name = name;`

`}`

`Programmer.prototype = **new**` `Person();`

`Programmer.prototype.coding = **function**(){`

`**return**` `"hello world";`

`}`

**`var`** `p1 = **new**` `Programmer('egoing');`

`document.write(p1.introduce()+"<br />");` // my name is egoing

`document.write(p1.coding()+"<br />");`  // hello world


=88번 영상===========================================

prototype : prototype이란?

[https://opentutorials.org/module/532/6573](https://opentutorials.org/module/532/6573)

prototype = 상속의 구체적인 수단이다.

prototype은 말 그대로 객체의 원형이라고 할 수 있다.

함수는 객체다. 그러므로 생성자로 사용될 함수도 객체다. 

객체는 프로퍼티를 가질 수 있는데 prototype이라는 프로퍼티는 

그 용도가 약속되어 있는 특수한 프로퍼티다. 

prototype에 저장된 속성들은 생성자를 통해서

객체가 만들어질 때 그 객체에 연결된다.

**`function`** `Ultra(){}`

`Ultra.prototype.ultraProp = **true**;`

**`function`** `Super(){}`

`Super.prototype = **new**` `Ultra();`

**`function`** `Sub(){}`

`Sub.prototype = **new**` `Super();`

**`var`** `o = **new**` `Sub();`

`console.log(o.ultraProp);`  // true


=89번 영상===========================================

prototype : prototype chain

 위 코드에서 생성자 Sub를 통해서 만들어진 객체 o가 

Ultra의 프로퍼티 ultraProp에 접근 가능한 것은 

prototype 체인으로 Sub와 Ultra가 연결되어 있기 때문이다. 

내부적으로는 아래와 같은 일이 일어난다.

1. 객체 o에서 ultraProp를 찾는다.
2. 없다면 Sub.prototype.ultraProp를 찾는다.
3. 없다면 Super.prototype.ultraProp를 찾는다.
4. 없다면 Ultra.prototype.ultraProp를 찾는다.

prototype는 객체와 객체를 연결하는 체인의 역할을 하는 것이다. 

이러한 관계를 prototype chain이라고 한다.


=90번 영상===========================================

표준 내장 객체의 확장 : 표준 내장 객체란?

[https://opentutorials.org/module/532/6475](https://opentutorials.org/module/532/6475)

표준 내장 객체(Standard Built-in Object)는 

자바스크립트가 기본적으로 가지고 있는 객체들을 의미한다. 

내장 객체가 중요한 이유는 프로그래밍을 하는데 

기본적으로 필요한 도구들이기 때문에다.

자바스크립트는 아래와 같은 내장 객체를 가지고 있다.

- Object
- Function
- Array
- String
- Boolean
- Number
- Math
- Date
- RegExp


=91번 영상===========================================

표준 내장 객체의 확장 : 배열의 확장1

배열을 확장해보자. 

아래 코드는 배열에서 특정한 값을 랜덤하게 추출하는 코드다.

**`var`** `arr = **new**` `Array('seoul','new york','ladarkh','pusan', 'Tsukuba');`

**`function`** `getRandomValueFromArray(haystack){`

`**var**` `index = Math.floor(haystack.length*Math.random());`// 스택길이x난수

`**return**` `haystack[index];` 

`}`

`console.log(getRandomValueFromArray(arr));` // 배열 중 랜덤으로 하나 출력


=92번 영상===========================================

표준 내장 객체의 확장 : 배열의 확장2

prototype을 사용해 위와 같은 것을 구현.

가독성이 더 좋아졌다.

`Array.prototype.rand = **function**(){`

`**var**` `index = Math.floor(**this**.length*Math.random());`

`**return**` **`this**[index];`

`}`

**`var`** `arr = **new**` `Array('seoul','new york','ladarkh','pusan', 'Tsukuba');`

`console.log(arr.rand());`   // 배열 중 랜덤으로 하나 출력


=93번 영상===========================================

Object : Object란?

[https://opentutorials.org/module/532/6578](https://opentutorials.org/module/532/6578)

Object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체이다. 

다시 말해서 아무것도 상속받지 않는 순수한 객체다. 

자바스크립트에서는 값을 저장하는 기본적인 단위로 Object를 사용한다.

**`var**grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};`

동시에 자바스크립트의 모든 객체는 Object 객체를 상속 받는데, 

그런 이유로 모든 객체는 Object 객체의 프로퍼티를 가지고 있다.


=94번 영상===========================================

Object : Object API

object 객체의 메뉴얼 읽는 법. 

다음 페이지에서 원하는 객체를 찾아 읽고 사용.

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

ex) 메뉴얼 예시

- Object.key() 페이지.
    
    [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
    
- Object.prototype.toString() 페이지
    
    [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)
    

![Untitled](/images/java_Script/Untitled%2064.png)

p.s) specification 란에서 버전 확인 가능.

     명시된 버전에서만 객체 사용 가능.


=95번 영상===========================================

Object : Object 확장

object, prototype 으로 배열에 포함된 문자 찾기 기능 제작.

`Object.prototype.contain = **function**(neddle) {`//needle:바늘찾기로 작명

`**for**(**var**` `name **in**` **`this**){`

`**if**(**this**[name] === neddle){`

`**return**` **`true**;`

`}`

`}`

`**return**` **`false**;`

`}`

**`var`** `o = {'name':'egoing', 'city':'seoul'}`

`console.log(o.contain('egoing'));`  // true

**`var`** `a = ['egoing','leezche','grapittie'];`

`console.log(a.contain('leezche'));` // true


=96번 영상===========================================

Object : Object 확장의 위험

위 코드와 같은 확장은 위험하다.

모든 코드에 영향을 주기 때믄이다.

따라서 해당사용법에는 주의를 기울여야 한다.

**`for**(var name **in**` `o){`

`console.log(name);`

`}` // name

         contain

객체가 기본적으로 가지고 있을 것으로 예상하고 있는 객체 외에 

다른 객체를 가지고 있는 것은 개발자들에게 혼란을 준다. 

이 문제를 회피하기 위해서는 프로퍼티의 해당 객체의 소속인지를

 체크해볼 수 있는 hasOwnProperty를 사용하면 된다.

**`for**(**var**` `name **in**` `o){`

`**if**(o.hasOwnProperty(name))`

`console.log(name);`

`}`

hasOwnProperty는 인자로 전달된 속성의 이름이 

객체의 속성인지 여부를 판단한다.

만약 prototype으로 상속 받은 객체라면 false가 된다

.


=97번 영상===========================================

데이터 타입 : 원시 데이터 타입과 객체

[https://opentutorials.org/module/532/6579](https://opentutorials.org/module/532/6579)

데이터 타입이란 데이터의 형태를 의미한다. 

데이터 타입은 크게 두가지로 구분할 수 있다. 

객체와 객체가 아닌 것. 

객체 데이터 타입 vs 원시 데이터 타입(primitive)

객체가 아닌 것 = 원시 데이터 타입

- 숫자
- 문자열
- 불리언(true/false)
- null
- undefined


=98번 영상===========================================

데이터 타입 : 래퍼 객체

래퍼 객체.

`var str = 'coding';`

`console.log(str.length);        //` `6`

`console.log(str.charAt(0));     //` `"C"`

문자열은 분명히 프로퍼티와 메소드가 있다. 

그렇다면 객체다. 

그런데 왜 문자열이 객체가 아니라고 할까? 

그것은 내부적으로 문자열이 원시 데이터 타입이고 

문자열과 관련된 어떤 작업을 하려고 할 때 

자바스크립트는 임시로 문자열 객체를 만들고 

사용이 끝나면 제거하기 때문이다.  

**`var`** `str = 'coding';`

`str.prop = 'everybody';`

`console.log(str.prop);      // undefined`

tr.prop를 하는 순간에 자바스크립트 내부적으로 String 객체가 만들어진다. 

prop 프로퍼티는 이 객체에 저장되고 이 객체는 곧 제거 된다. 

그렇기 때문에 prop라는 속성이 저장된 객체는 존재하지 않게된다. 

이러한 특징은 일반적인 객체의 동작 방법과는 다르다.

하지만 문자열과 관련해서 필요한 기능성을 

객체지향적으로 제공해야 하는 필요 또한 있기 때문에 

원시 데이터 형을 객체처럼 다룰 수 있도록 하기 위한 객체를 

자바스크립트는 제공하고 있는데 그것이 레퍼객체(wrapper object)다.


=99번 영상===========================================

참조 : 복제란?

[https://opentutorials.org/module/532/6507](https://opentutorials.org/module/532/6507)

전자화된 시스템의 가장 중요한 특징은 복제다. 

현실의 사물과 다르게 전자화된 시스템 위의 데이터를 

복제 하는데는 비용이 거의 들지 않는다. 

이 특징이 소프트웨어를 기존의 산업과 구분하는 가장 큰 특징일 것이다. 

프로그래밍에서 복제가 무엇인가를 살펴보자.

**`var`** `a = 1;`

**`var`** `b = a;`

`b = 2;`

`console.log(a); // 1`


=100번 영상===========================================

참조 : 참조

그런데 자연의 산물이 아니라 거대한 약속의 집합인 

소프트웨어의 세계에서 당연한 것은 없다. 

이것이 당연하지 않은 이유는 다음 예제를 통해서 좀 더 분명하게 드러난다.

`var a = {'id':1};`

`var b = a;`

`b.id = 2;`

`console.log(a.id);  // 2`

변수 b에 담긴 객체의 id 값을 2로 변경했을 뿐인데 a.id의 값도 2가 되었다. 

이것은 변수 b와 변수 a에 담긴 객체가 서로 같다는 것을 의미하다. 

이것은 참조(reference)로 인한 결과이다.

비유하자면 복제는 파일을 복사하는 것이고 

참조는 심볼릭 링크(symbolic link) 혹은 

바로가기(윈도우)를 만드는 것과 비슷하다. 

원본 파일에 대해서 심볼릭 링크를 만들면 

원본이 수정되면 심볼릭 링크에도 

그 내용이 실시간으로 반영되는 것과 같은 효과다. 

다시 말해서 원본을 복제한 것이 아니라 

원본 파일을 참조(reference)하고 있는 것이다. 

덕분에 저장 장치의 용량을 절약할 수 있고, 

원본 파일을 사용하고 있는 모든 복제본이 동일한 내용을 유지할 수 있게 된다. 

`a = 1;`

`a = {'id':1};`

전자는 데이터형이 숫자이고 후자는 객체다. 

숫자는 원시 데이터형(기본 데이터형, Primitive Data Types)이다. 

자바스크립트에서는 원시 데이터형을 제외한 모든 데이터 타입은 객체이다. 

객체를 다른 말로는 참조 데이터 형(참조 자료형)이라고도 부른다. 

기본 데이터형은 위와 같이 복제 되지만 참조 데이터형은 참조된다. 

모든 객체는 참조 데이터형이다.


=101번 영상===========================================

참조 : 함수와 참조

일종의 변수할당이라고 할 수 있는 메소드의 매개변수는 

어떻게 동작하는가를 살펴보자.

다음은 원시 데이터 타입을 인자로 넘겼을 때의 동작 모습이다.

**`var`** `a = 1;`

**`function`** `func(b){`

`b = 2;`

`}`

`func(a);`

`console.log(a);`  // 1

다음은 참조 데이터 타입을 인자로 넘겼을 때 동작하는 장면이다.

`var a = {'id':1};`

`function func(b){`

`b = {'id':2};`

`}`

`func(a);`

`console.log(a.id);  // 1`

함수 func의 파라미터 b로 전달된 값은 객체 a이다. 

(b = a) b를 새로운 객체로 대체하는 것은 (b = {'id':2}) 

b가 가르키는 객체를 변경하는 것이기 때문에 객체 a에 영향을 주지 않는다.

하지만 다음은 다르다.

**`var`** `a = {'id':1};`

**`function`** `func(b){`

`b.id = 2;`

`}`

`func(a);`

`console.log(a.id);  // 2`

파라미터 b는 객체 a의 레퍼런스다. 

이 값의 속성을 바꾸면 그 속성이 소속된 객체를 대상으로 

수정작업을 한 것이 되기 때문에 b의 변경은 a에도 영향을 미치게 된다.

시간나면 다음 영상을 참조하라.

코드와 오픈소스 :

[https://opentutorials.org/course/1189/6340](https://opentutorials.org/course/1189/6340)


=102번 영상===========================================

수업을 마치며.

1.코드는 양면테이프와 같다.

부품과 부품을 이어붙여 편의성을 도모할 수 있다.

하지만 이제는 테이프에서 벗어나 부품 그 자체에도 주의를 기울여야 한다.

2.문법을 많이 알아둬야 한다.

다른 사람의 코드를 이해하기 쉬워지고 실력향상에 도움이 된다.

3.가장 본질적인 언어 하나를 붙잡고 결과물을 만들어라.

본질적인 언어란 단순히 절차에 따라 사건이 일어나게 하는 것이다.

끝.