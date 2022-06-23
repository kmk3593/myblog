---
title: "Java Script 기초"
tags:
  - setting
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-07'
---

### 사전작업

- 살행할 폴더 우클릭 : git bash here
- VSCord 작동 : `code .`

- 폴더, 파일 생성
- PROJECT 아래에 생성
    - 폴더 생성 : step03_js_basic
    - 파일 생성 : index.html
    - 파일 생성 : main.js

### JavaScript 작성

- index.html 에 다음 내용 작성

```html
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width">
    <title>Document</title>
    <script src="./main.js"></script>
</head>

<body>
    <h1>자바스크립트 연습</h1>
</body>

</html>
```

- main.js에 다음 내용 작성

```jsx
// hello world
console.log("hello!")
```

- step03_js_basic 폴더에서 index.html을 오픈
- 다음과 같이 페이지가 출력된다.

![Untitled](/images/javaScript_start/Untitled.png)

### 시스템 로그

- main.js 에 다음 내용 작성

```jsx
// hello world
console.log("Hello!!!");

// 변수명 작성 스타일
// camel Case : numOne

const myName = "kmk";
const email = "abc@gmail.com";
const hello = '안녕 ${myName}!';

// print()
console.log(myName);
console.log(email);
console.log(hello);
```

- html 페이지에서 우클릭 → 검사
- 다음과 같이 시스템 로그가 출력되었다.

![Untitled](/images/javaScript_start/Untitled%201.png)

### key-value

- key-value를 비롯한 여러 변수를 호출해본다.
- main.js 에 다음 내용 작성

```jsx
// hello world
console.log("Hello!!!");

// 변수명 작성 스타일
// camel Case : numOne

const myName = "kmk";
const email = "abc@gmail.com";
const hello = '안녕 ${myName}!';

// print()
console.log(myName);
console.log(email);
console.log(hello);

// 숫자
const number = 123;
console.log(number)

// Boolean
let checked = true;
let isShow = false;
console.log(checked)
console.log(isShow)

//undefied
let abc;
console.log(abc);

//null
let name = null;
console.log(name);

//재할당
name = 'kmk';
console.log(name);

// 파이썬 딕셔너리와 비슷
// key-value
const user = {
    name: 'kmk',
    age: 20,
    isValid: true 
}

console.log(user.name);
console.log(user.age);
console.log(user.isValid);
// console.log(user.user.city);  undefined
```

- 다음과 같이 시스템 로그가 출력된다.

![Untitled](/images/javaScript_start/Untitled%202.png)

### 사칙 연산

- main.js 에 다음 내용 추가

```jsx
// 사칙 연산
const a=2;
const b=5;
console.log(a + b);
console.log(a - b);
console.log(a * b);
console.log(a / b);
```

- 연산 결과가 시스템 로그에 출력된다.

![Untitled](/images/javaScript_start/Untitled%203.png)

### 함수 선언과 호출

- main.js 에 다음 내용 추가

```jsx
// 함수의 선언과 호출
function helloFunc() {
    console.log(1234);
}

helloFunc();

function returnFunc() {
    return 123;
}

const fun_result = returnFunc();
console.log(fun_result);

function sum(a, b){
    return a + b;
}

const sum_a = sum(1, 2);
console.log(sum_a);

const sum_b = sum(4,5)
console.log(sum_b);

// anonymous(익명 함수)
const world = function(){
    console.log("We are the world");
}
world();
```

- 결과가 시스템 로그에 출력된다.

![Untitled](/images/javaScript_start/Untitled%204.png)

### 조건문

- main.js 에 다음 내용 추가

```jsx
// 조건문
const isDone = false;
if (isDone) {
    console.log('done!')
} else {
    console.log('Not Yet')
}
```

- 결과가 시스템 로그에 출력된다.

![Untitled](/images/javaScript_start/Untitled%205.png)