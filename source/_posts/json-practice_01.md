---
title: "JSON"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-20'
---



- JSON : JavaScript Object Notation
- 2차원 데이터를 관리하기 쉬운 JavaScript 타입.

[실습 예제]

![Untitled](/images/json-practice_01/Untitled.png)

### 데이터 관리의 방법 - CSV, XML, JSON

- 데이터 관리 방법 : CSV, XML, JSON
- 브라우져에서 해석하기 쉬운 JSON 방식으로 많이 사용함

![Untitled](/images/json-practice_01/Untitled%201.png)

### JSON Parse 예제

- 문자열로 들어온 JSON 데이터를 Parse를 통해서 데이터 관리 할 수 있다
- 파싱 : 각 문장의 문법적인 구성 또는 구문을 분석하는 과정.

[실습 예제]

![Untitled](/images/json-practice_01/Untitled%202.png)

### 연산자

- Java Script의 연산자

![Untitled](/images/json-practice_01/Untitled%203.png)

- 값의 비교 : == 또는 !=
- 주소의 비교 : === 또는 !==

![Untitled](/images/json-practice_01/Untitled%204.png)

### 제어구조

- JavaScript의 제어구조

![Untitled](/images/json-practice_01/Untitled%205.png)

- 제어구조 예시

![Untitled](/images/json-practice_01/Untitled%206.png)

### 함수

- JAVA 스크립트는 함수는 있으나 다른 언어처럼 정의하지는 않고, 만드는 형태

![Untitled](/images/json-practice_01/Untitled%207.png)

### 함수 사용해보기

- 여러가지 방식으로 함수를 사용해보자

```html
<script>
        document.write("함수 사용하는 여러가지 방법")
        document.write("<BR>");

        let add1 = new Function ("x,y", "return x+y");
        document.write(add1(3,4));
        document.write("<BR>");
        
        let add2 = function (x,y){
            return x+y;
        }
        document.write(add2(3,4));
        document.write("<BR>");

        function add3(x,y){
            return x+y;
        }
        document.write(add3(3,4));

        function add4(x,y){
            document.write(arguments);
            document.write("<BR>");
            document.write(arguments[0], arguments[1], arguments[5]); 
            document.write("<BR>");
            return x+y;
        }
        document.write(add4(3,4,5,6,7,"HUMAN")); //7

    </script>
```

- 다음과 같은 결과가 출력된다

![Untitled](/images/json-practice_01/Untitled%208.png)

### 함수 - 지역변수, 전역변수

- 변수 선언 : var, let, const임
- var가 포함되지 않은 변수는 전역변수로 활용됨. (window.변수명)

![Untitled](/images/json-practice_01/Untitled%209.png)

### Browser 플랫폼

- 브라우져 플랫폼 : 브라우져 객체를 활용
- 브라우져 객체 핸들링을 통해서 브라우져의 활용이 가능함

![Untitled](/images/json-practice_01/Untitled%2010.png)

### Browser 플랫폼 -사용자와 상호작용 가능한 메서드

- alert : 사용자에게 알람을 주는 메서드
- prompt : 사용자에게 입력을 받는 메서드
- confirm : 사용자의 선택을 확인하는 메서드

![Untitled](/images/json-practice_01/Untitled%2011.png)

### 상호작용 - 입력 받은 값으로 실행

- 코드를 작성해보자

```html
<script>
        let x,y;
        // x = window.prompt ("x값 입력 = ", 0);
        // y = window.prompt ("y값 입력 = ", 0);

        // window는 생략 가능
        x=eval(prompt("x 값 입력 = ", 0)); 
        y=eval(prompt("y 값 입력 = ", 0)); 
        alert(x+y);

        // 정수형으로 변환
        x=parseInt(prompt("x 값 입력 = ", 0)); 
        y=parseInt(prompt("y 값 입력 = ", 0)); 
        alert(x+y);

        // 실수형으로 변환
        x=parseFloat(prompt("x 값 입력 = ", 0)); 
        y=parseFloat(prompt("y 값 입력 = ", 0)); 
        alert(x+y);

        let answer;
        answer = confirm("정말로 삭제하시겠습니까?");
        document.write(answer);
        document.write("<BR>");
        if(answer) 
						document.write("삭제");
        else
						document.write("취소");
    </script>
```

- 결과는 다음과 같다

![Untitled](/images/json-practice_01/Untitled%2012.png)

- confirm이 어떤 식으로 적용되는지 확인

![Untitled](/images/json-practice_01/Untitled%2013.png)

### Browser 플랫폼 -이벤트 기반 프로그래밍

- 사용자 이벤트에 의해 처리하는 방식
- 사용자 이벤트 : Keyboard 입력 / 마우스 move / 마우스 클릭 등

![Untitled](/images/json-practice_01/Untitled%2014.png)

### Browser 플랫폼 – 이벤트 기반 함수호출

- 사용자 이벤트를 함수적으로 호출하여 프로그램의 간소화 가능

![Untitled](/images/json-practice_01/Untitled%2015.png)

### Browser 플랫폼 - 객체 활용하여 HTML 문서로 변경

- 윈도우 객체에 값 전달하여 HTML 문서의 변경

![Untitled](/images/json-practice_01/Untitled%2016.png)

### Button

- 버튼을 사용해보자
- 버튼을 누르면 함수가 적용되도록 작성
- 버튼을 누르고 나면 텍스트창으로 변환되도록 의도

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        function printResult1(){
            let x, y;
            x = eval(prompt ("x값 입력 = ", 0));
            y = eval(prompt ("y값 입력 = ", 0));
            alert (x+y);
        }
        
        function printResult2(){
            let x, y;
            x = eval(prompt ("x값 입력 = ", 0));
            y = eval(prompt ("y값 입력 = ", 0));
            btn1.value = x+y;
            btn1.type = "text";
        }
    </script>
</head>
<body>
    <input type="button" value="클릭1" onclick="alert('안녕하세요');">
    <input type="button" value="클릭2" onclick="printResult1();">
    <input type="button" value="클릭3"
    onclick="printResult2();" id="btn1">
</body>
</html>
```

### Browser 플랫폼 – 여러 스크립트 활용시 문제점

- 윈도우 객체에 값 전달하여 HTML 문서의 변경

![Untitled](/images/json-practice_01/Untitled%2017.png)

### Browser 플랫폼 – getElementById

- getElementById : 엘리먼트(일반적으로 tag) ID를 통한 엘리먼트 객체 획득

![Untitled](/images/json-practice_01/Untitled%2018.png)

### Browser 플랫폼 – onload시 2개의 함수 호출방법

- onload를 통해 1개의 함수 호출은 가능하나 2개의 기능을 순차적 실행은 불가함.
- 이럴 때는 addEventListener를 통해서 처리 가능

![Untitled](/images/json-practice_01/Untitled%2019.png)

- addEventListener를 사용해보자
- html파일을 작성하고 함께 사용할 js파일도 작성한다

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="Js_Exam_15_1.js"></script>
    <script src="Js_Exam_15_2.js"></script>
</head>
<body>
    <input type="button" value="클릭5" id="btn5">
</body>
</html>
```

- Js_Exam_15_1.js

```html
// window.onload = function(){
window.addEventListener("load", function(){
    let printBtn = window.document.getElementById("btn5");
    printBtn.onclick = function(){
        let x,y;
        x=eval(prompt ("x값 입력 = ", 0));
        y=eval(prompt ("y값 입력 = ", 0));
        btn5.type = "text";
        btn5.value = x+y;
    };    
}
);
```

- Js_Exam_15_2.js

```html
// alert("Hi, 휴먼교육센터");

window.addEventListener("load", function(){
    alert("Hi, 휴먼교육센터");
});
```

- 결과 - 두 js파일에 담긴 기능이 모두 구현되었다.

![Untitled](/images/json-practice_01/Untitled%2020.png)

### 계산기 만들기

- 간단한 계산기를 만들어보자
- 일단 (+) 기능부터 시작
- calc_01.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>계산기</title>
    <script src="calc_01.js"></script>
</head>
<body>
    <input type = "text" id = "txt1"> +
    <input type = "text" id = "txt2"> 
    <input type = "button" id = "add" value="="> 
    <input type = "text" id = "sum" value = 0> 
    
</body>
</html>
```

- calc_01.js

```html
window.addEventListener("load", function(){
    let btnPrint = this.document.getElementById("add");
    btnPrint.onclick = function(){
        let x, y;
        x = parseInt(document.getElementById("txt1").value);
        y = parseInt(document.getElementById("txt2").value);
        sum.value = x+y;

    };
});
```

- (+) 기능이 구현되었다

![Untitled](/images/json-practice_01/Untitled%2021.png)