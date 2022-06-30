---
title: "Java Script 실습3"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-11'
---


### 사전작업

- 살행할 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step05_js
    - 파일 생성 : ch03_variables.html

### JavaScript 작성

- ch03_variables.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <h1 id = "string">Hello World!</h1>
        <h1 id = "number"> 123 </h1>
    </center>
    <script>
        var firstName = "evan";
        var ageNum = 30;
        document.getElementById('string').innerHTML = firstName;
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch03_variables.html을 오픈
- 페이지가 출력된다.

![Untitled](/images/javaScript_practice_3/Untitled.png)

### 연산 결과 출력

- ch04_math_js.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document4</title>
</head>
<body>
    <center>
        <h1 id = "string">Hello World!</h1>
        <h1 id = "addition"> 123 </h1>
    </center>
    <script>
        /*
            사칙연산 구현하기
        */
        var num_1 = 10;
        var num_2 = 20;
        document.getElementById('addition').innerHTML = num_1 + num_2;
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch04_math_js.html을 오픈
- 페이지에 연산 결과인 30이 출력된다.

![Untitled](/images/javaScript_practice_3/Untitled%201.png)

### 연산 결과 출력(boolean)

- ch05_operators.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document4</title>
</head>
<body>
    <center>
        <h1 id = "string">Hello World!</h1>
        <h1 id = "addition"> 123 </h1>
    </center>
    <script>
        /*
            사칙연산 구현하기
        */
        var num_1 = 10;
        var num_2 = 20;
        document.getElementById('addition').innerHTML = num_1 + num_2;
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch05_operators.html을 오픈
- 페이지에 연산 결과인 true, false가 출력된다.

![Untitled](/images/javaScript_practice_3/Untitled%202.png)

### 조건문

- ch06_conditional.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <h1 id = "demo"> your_domain </h1>
    </center>
    <script>
        firstName = "john";

        if(firstName = "john"){
            document.getElementById("demo").innerHTML = firstName;
        } else if (firstName = "ddd") {
            document.getElementById("demo").innerHTML = "Hello my name is!";
        } else {
            document.getElementById("demo").innerHTML = "이름이 다름!";
        }
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch06_conditional.html을 오픈
- 페이지에 조건문에 의한 결과 출력

![Untitled](/images/javaScript_practice_3/Untitled%203.png)

### 다중 조건문

- ch07_multiple_condition.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <h1 id = "demo"> your_name </h1>
    </center>
    <script>
        firstName = "ABC";
        ageNum = 30;
        // %% --> AND
        // || --> OR

        if(firstName = "John" && ageNum == 30){
            document.getElementById('demo').innerHTML = firstName;
        } else if (firstName = "my name is") {
            document.getElementById("demo").innerHTML = "Hello my name is!";
        } else {
            document.getElementById("demo").innerHTML = "이름이 다름!";
        }
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch07_multiple_condition.html을 오픈
- 페이지에 조건문에 의한 결과 출력

### 반복문

- ch08_arrays.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
    <center>
        <h1 id = "demo">arrays</h1>
    </center>
    <script>
        var pizzaToppings = ['Pepperoni', 'Mushroom', 'Sausage', 'cheese'];
        for (i=0; i < pizzaToppings.length; i++) {
            document.write(pizzaToppings[i] + '<br/>');
        }
    </script>
</body>
</html>
```

- step05_js 폴더에서  ch08_arrays 오픈
- 반복문에 의한 결과 출력

![Untitled](/images/javaScript_practice_3/Untitled%204.png)

### 입력

- ch09_prompt.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./js/myscript.js"></script>
</head>
<body>
    <center>
        <h1 id = "demo">Prompt</h1>
    </center>
    <script>
        var yourName = prompt("이름을 적어주세요!!");
        console.log(yourName);
        document.write(hello(yourName));
    </script>
</body>
</html>
```

- myscript.js 에 다음 코드 작성

```jsx
document.getElementById('demo').innerHTML="자바스크립트";

function hello(firstName) {
    return "안녕하세요!" + firstName;
}
```

- step05_js 폴더에서  ch09_prompt.html 오픈
- 입력 프롬프트 출력

![Untitled](/images/javaScript_practice_3/Untitled%205.png)

### 난수

- ch10_random_num.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./js/myscript.js"></script>
</head>
<body>
    <center>
        <h1 id = "demo">Random Numbers</h1>
    </center>
    <script>
        document.write(Math.floor(Math.random() * 100 ) + 1);
    </script>
</body>
</html>
```

- step05_js 폴더에서 ch10_random_num.html 오픈
- 난수 출력

![Untitled](/images/javaScript_practice_3/Untitled%206.png)

### 입력과 출력

- ch11_web_forms.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="./js/myscript2.js"></script>
</head>
<body>
    <center>
        <h1 id = "demo">Input , Output</h1>
    </center>
    <p>안녕하세요, 이름을 입력하세요:</p>
    <input id = "name">
    <button type="button" onclick="hello()">제출</button>
    <p id = "output"></p>
</body>
</html>
```

- 파일 생성
- project/step05_js/js 아래에 생성
    - 파일 생성 : myscript2.js
    - 다음 코드를 작성한다.

```jsx
// Functions
function hello() {
    var firstName = document.getElementById('name').value;
    document.getElementById('output').innerHTML = "정답 :  " + firstName;
}
```

- step05_js 폴더에서 ch11_web_forms.htmll 오픈
- 입력하면 후 출력이 가시적으로 표현된다.

![Untitled](/images/javaScript_practice_3/Untitled%207.png)

### 계산기(더하기)

- ch12_flash_cards.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="./js/myscript2.js"></script>

</head>

<body>
    <br />
    <center>
        <h1 id="demo">
            <script>
                var numOne = Math.floor(Math.random() * 10) + 1;
                var numTwo = Math.floor(Math.random() * 10) + 1;

                document.write(numOne + " + " + numTwo); 

                // 계산 결과
                // console.log(correctAnswer);

                var correctAnswer = numOne + numTwo;
                /*
                document.write(Math.floor(Math.random() * 10) + 1);
                document.write(" + ");
                document.write(Math.floor(Math.random() * 10) + 1);
                */
            </script>
        </h1>
    <p>답변을 입력하세요:</p>
    <input id="answer">
    <button type="button" onclick="addition()">제출</button>
    <input type="button" value = "새로운 문제 클릭!" onclick="newCard()">
    <br /><br />
    <p id="output"></p>
    <p id="solution"></p>
    </center>
</body>

</html>
```

- myscript2.js 에 다음 코드 작성

```jsx
// Functions
function hello() {
    var firstName = document.getElementById('name').value;
    document.getElementById('output').innerHTML = "정답 :  " + firstName;
}

// addition()
function addition() {
    var ourAnswer = document.getElementById("answer").value;
    console.log(ourAnswer);

    // 문자열 처리
    if (isNaN(ourAnswer)) {
        document.getElementById("output").innerHTML = "입력한 " + ourAnswer + "는 숫자가 아닙니다!";

    // 숫자 처리
    } else {
        // 정답일 때,
        document.getElementById("output").innerHTML = ourAnswer;
        if(ourAnswer == correctAnswer) {
            document.getElementById("solution").innerHTML = "정답입니다!";
        } else { // 정답이 아닐 때,
            document.getElementById("solution").innerHTML = "정답이 아닙니다!";
        }
    }
}

function newCard() {
    document.getElementById('output').innerHTML = ""
    document.getElementById('answer').value = ""
    document.getElementById('solution').innerHTML = ""
    numOne = Math.floor(Math.random() * 10) + 1;
    numTwo = Math.floor(Math.random() * 10) + 1;

    document.getElementById('demo').innerHTML = numOne + " + " + numTwo;
    correctAnswer = numOne + numTwo;

}
```

- step05_js 폴더에서 ch12_flash_cards.htm 오픈
- 더하기 한정으로 계산 기능이 구현되었다.

![Untitled](/images/javaScript_practice_3/Untitled%208.png)

![Untitled](/images/javaScript_practice_3/Untitled%209.png)