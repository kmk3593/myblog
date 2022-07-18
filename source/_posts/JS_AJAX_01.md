---
title: "JavaScript AJAX"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-07-02'
---


### 프로그램 언어별 포지션

- Front-End : Web Browser 등 사용자와 접점을 가지고 있는 부분을 개발
- Back-End : 데이터 기반의 로직을 기반으로 솔루션의 엔진을 담당

![Untitled](/images/JS_AJAX_01/Untitled.png)

### JAVA 언어의 단계

- 현재 취업시장에서 가장 많은 것은 웹 프로그래머
- 웹 프로그램은 서블릭 ➔ JSP ➔ Spring의 단계로 교육이 진행될 예정

![Untitled](/images/JS_AJAX_01/Untitled%201.png)

### 비동기(Asynchronous) 통신이란?

- AJAX (Asynchronous Javascript And XML) : XHR(XMLHttpRequest), AXIOS, FETCH 방식
- 비동기 애플리케이션을 만들기 위해 클라이언트에서 단에서 쓰이는 웹개발 기술들.

![Untitled](/images/JS_AJAX_01/Untitled%202.png)

### 비동기 통신의 탄생배경

- 기존 웹문서는 구조가 바뀌면 모든 문서를 변경해야 하는 한계가 있음. (유지관리 비용 증가)
- 한계를 극복하고자 비동기 통신이 탄생함

![Untitled](/images/JS_AJAX_01/Untitled%203.png)

### 비동기 통신 구현 원리

- innerHTML을 활용하여 이벤트 발생시 article 태그에 문서를 삽입한다
- 문서 삽입은 querySelector를 활용
- ajax_01.html 일부

```html
<body>
    <ol>
        <li><a onclick="document.querySelector('article').innerHTML='<h1>HTML</h1><P>HTML is ....</P>';">
            HTML</a></li>
         
        <li><a onclick="document.querySelector('article').innerHTML='<h1>CSS</h1><P>CSS is ....</P>';">
            CSS</a></li>
        
        <li><a onclick="document.querySelector('article').innerHTML='<h1>JAVA Script</h1><P>JAVA Script is ....</P>';">
            JAVA Script</a></li>
    </ol>
    <article>
    </article>
</body>
```

- 결과

![Untitled](/images/JS_AJAX_01/Untitled%204.png)

### 비동기 통신 구현을 위한 TEST - 1

- callback 함수를 통한 로그 확인. (JAVASCRIPT 문서 확인함.)
- 로그가 먼저 찍히고, response OK가 됨. (비동기식이므로)

![Untitled](/images/JS_AJAX_01/Untitled%205.png)

### 비동기를 결과를 확인

- 먼저 1 2 3 출력
- 그 다음에서야 response.OK!! 출력

![Untitled](/images/JS_AJAX_01/Untitled%206.png)

### 비동기 통신 구현을 위한 TEST - 2

- CSS 문서 확인하여 text란 변수에 넣어라.
- response.status = 200은 통신에 성공했다는 의미임

![Untitled](/images/JS_AJAX_01/Untitled%207.png)

### 5.4.3. 비동기 통신 구현을 위한 TEST - 3

- FETCH API는 전달하는 문서를 text로 받고, inner HTML을 통해 article tag에 문서를 포함
- 이 때 response 객체를 통해서 성공여부를 확인할 수 있음 (AJAX의 기본은 마무리)

![Untitled](/images/JS_AJAX_01/Untitled%208.png)

- 여기까지 작성했을 때의 코드
- ajax_02.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
   <input type ="button" value = "click callbackMe" 
        onclick="fetch('JAVASCRIPT').then(callbackme);
                function callbackme(){
                    console.log('response. OK!!');
                };
                console.log(1);
                console.log(2);
                console.log(3);
                "
    >
    <!-- JAVASCRIPT 문서를 읽으면, response라는 변수에 담아와라. -->
    <!-- response 변수의 text함수를 통해서 읽어온 값을 alert 해라.-->
    <input type="button" value="click AJAX" 
        onclick="fetch('HTML').then(function(response){
                    response.text().then (
                        function(text) {
                            alert(text);
                            console.log(response);
                            console.log(response.ok);  // true, false
                            console.log(response.status);// 200은 성공, 404는 페이지 못찾음
                    })
        });"
    >
    <input type="button" value="click AJAX_ERROR처리" 
        onclick="fetch('HTML').then(function(response){
                    response.text().then (
                        function(text) {
                            if (response.ok) {
                                // alert(text);
                                document.querySelector('article').innerHTML=text;
                                console.log('success');
                            }
                            else {
                                console.log('ERROR');
                            }
                    })
        });"
    >
    <article>

    </article>

</body>
</html>
```

- CSS
- 확장자없이 해당 이름으로만 만든 파일이다

```html
<h1>CSS</h1><P>CSS is ....</P>
```

- JAVASCRIPT
- 확장자없이 해당 이름으로만 만든 파일이다

```html
<h1>JAVA Script</h1><P>JAVA Script is ....</P>
```

- HTML
- 확장자없이 해당 이름으로만 만든 파일이다

```html
<h1>HTML</h1><P>HTML is ....</P>
```

- 결과
- 버튼을 1번씩 클릭했을 때 다음과 같은 결과가 출력된다

![Untitled](/images/JS_AJAX_01/Untitled%209.png)

### 비동기 통신 구현을 위한 TEST - 4

- 공통된 부분을 하나로 합쳐서 처리
- 위 코드를 다음 형태로 정리할 수 있다

![Untitled](/images/JS_AJAX_01/Untitled%2010.png)

### 실습

- Do it! 웹 사이트 따라 만들기 7장 p.214
- 우선 chrome → 우클릭 : 속성 → 대상에 다음 내용을 붙여넣는다.
    - exe” 이후에 띄어쓰고 붙이면 된다
    - `-allow-file-access-from-files`

![Untitled](/images/JS_AJAX_01/Untitled%2011.png)

