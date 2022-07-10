---
title: "JavaScript JQuery"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-27'
---
  
jQury를 사용해보자

### JQuery란?

- JQuery 사용이유 : 브라우저간 호환성 문제, CSS지원, 복잡한 HTML 문서를 단순화하는 용도
- 기본적으로 JAVA Script 문법을 기반으로 활용이 가능하다

![Untitled](/images/JS_JQuery/Untitled.png)

- 이 기종으로 관리되는 모든 Browser의 기능을 숨긴다
- Jquery Object를 통해서 Document Object를 관리

![Untitled](/images/JS_JQuery/Untitled%201.png)

### Jquery 셋업

- Jquery 라이브러리는 서버에 다운로드 하여 사용하는 방법과 CDN을 활용하는 방법이 있음
- CDN : Content Delivery Network
1. 각 주요 사이트별로 호스팅하고 있는 CDN이 있음.
2. CDN을 이용하는 것이 효율적인 이유는
다른 사이트도 Jquery로 개발된 사이트가 많다보니
Cash에 대부분 CDN 사이트 로부터 받아놓은 것이 있을 수 있음.
3. 단, 다운로드도 받아놓는 것은 인터넷이 끊기거나.
호스팅 사이트가 사라질 수도 있는데. 이 때 주소만 바꾸면 되며
보험용으로 라이브러리로 다운로드 받아서 관리하고 있으면 좋음

### 설치

- Jquery

[https://jquery.com/](https://jquery.com/)

![Untitled](/images/JS_JQuery/Untitled%202.png)

- download 탭으로 이동
- [https://jquery.com/download/](https://jquery.com/download/)
- 우클릭 → 다른 이름으로 저장

![Untitled](/images/JS_JQuery/Untitled%203.png)

- Download 탭에서 아래로 스크롤
- Google CDN 이동

![Untitled](/images/JS_JQuery/Untitled%204.png)

- [https://developers.google.com/speed/libraries#jquery](https://developers.google.com/speed/libraries#jquery)
- 해당하는 버전을 카피해서 사용한다

![Untitled](/images/JS_JQuery/Untitled%205.png)

- 다음과 같은 형태로 사용

```html
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

</head>
```

### Jquery 시작하기

- Jquery 맛보기
- jquery는 chain의 형태로 대상과 대상이 해야할 일에 대해서 처리

![Untitled](/images/JS_JQuery/Untitled%206.png)

### 선택자

- 선택자를 활용하여 선택된 대상에 CSS를 적용할 수 있다

![Untitled](/images/JS_JQuery/Untitled%207.png)

### 선택자 실습

- 선택자를 사용해본다
- jquery_test_02.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script>
        // 모든 문서가 로드가 되면..
        $(function(){
            // 직접선택자
            $(".wrap-1").css("border","1px solid orange");
            $(".wrap-1 p").css("background","yello");
            // 근접선택자
            $(".active").next("p").css("background", "aqua");
            // 위치선택자
            $(".wrap-1 p").eq(1).css("font-size","5px");
            // 속성선택자
            $("input[type-text]").css("background","orange");
            // 객체조작 ==> class="active" 제거. aqua 컬러 미적용
            $(".wrap-1 p").eq(1).removeClass("active");
            $(".active").next("p").css("background", "aqua");
            // 객체조작 ==> class="active" 추가. aqua 컬러 적용
            $(".wrap-1 p").eq(1).addClass("active");
            $(".active").next("p").css("background", "aqua");
            // 객체조작 ==> tag를 추가함
            
            $(".wrap-1 p").append("<p>휴먼교육센터</p>");
        });
    </script>
</head>
<body>
    <div class="wrap-1">
        <p>텍스트1</p>
        <p class="active">내용2</p>
        <p><a href="https://www.naver.com/">네이버</a></p>
        <p><input type="text" value="hello"></p>
    </div>
    <div class = "wrap-2">
        <p>내용5</p>
        <p>내용6</p>
    </div>
</body>
</html>
```

- 결과

![Untitled](/images/JS_JQuery/Untitled%208.png)

### 이벤트 핸들링

- Jquery 는 발생하는 이벤트를 체크하여 문서를 관리할 수 있음

![Untitled](/images/JS_JQuery/Untitled%209.png)

### 이벤트 핸들링 실습

- jquery_test_03.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script>
        // 모든 문서가 로드가 되면..
        $(function(){
            // $(".btn1 a").mouseover(function(){
            //     alert("휴먼교육센터");
            // })
            
            // 2개 이상의 이벤트를 동시에 적용 가능 
            // $(".btn1 a").on("mouseover focus", function(){
            //     // 선택된 대상
            //     let ts = $(this);
            //     ts.css("background-color", "yellow");
            // });

            $(".btn1 a").on("mouseover focus", function(){
                // 선택된 대상
                let ts = $(this);
                // 선택된 대상의 ul 태그 중 visible이 포함된 것이라면 hide(숨기고)
                $(".btn1").next("ul").filter(":visible").hide();
                // 선택된 부모(p)의 다음 것을 출력
                ts.parent().next().show();
                return false;
 
            });
        });
    </script>
</head>
<body>
    <p class="btn1"><a href = "#">이벤트 대상1</a></p>
    <ul style="display:none">
        <li>리스트1</li>
        <li>리스트2</li>
        <li>리스트3</li>
    </ul>

    <p class="btn1"><a href = "#">이벤트 대상2</a></p>
    <ul style="display:none">
        <li>리스트4</li>
        <li>리스트5</li>
        <li>리스트6</li>
    </ul>

</body>
</html>
```

- 결과

![Untitled](/images/JS_JQuery/Untitled%2010.png)

### 효과 및 애니메이션

- Jquery 는 이벤트 발생시 효과 및 애니메이션 기능을 수행함
- 효과 메서드
    - 요소를 역동적으로 숨겼다 보이도록 해주는 매서드가 있다
    - 선택한 요소에 동적으로 적용 가능
- 효과 메서드 사용법
    - `$(요소 선택).효과 메서드(효과소요시간, 가속도, 콜백함수)`
- 애니메이션 사용법
    - `$(요소 선택).animate({적용할 속성과 값}, 가속도, 콜백함수);`
    

### 애니메이션 실습02

- jquery_04.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JQuery</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script>
        // 모든 문서가 로드가 되면...
        $(function(){
            $(".btn1").on("click", function(){
                let ts = $(this);
                if(ts.text() == "숨김") {
                    // 1000은 1초를 의미.
                    $(".wrap").slideUp(1000, function(){
                        $(".btn1").text("노출");
                    })
                }
                else{
                    $(".wrap").slideDown(1000, function(){
                        $(".btn1").text("숨김");

                    })
                }
            });
        });
    </script>
</head>
<body>
    <p class="btn-wrap">
        <button class="btn1">숨김</button>
    </p>
    <div class="wrap">
        <p class="txt1">내용1</p>
        <p class="txt1">내용2</p>
    </div>

    
</body>
</html>
```

- 결과
- 숨김 버튼을 누르면 텍스트가 사라지고 노출 버튼으로 전환
- 노출 버튼을 누르면 텍스트가 출력되고 숨김 버튼으로 전환

![Untitled](/images/JS_JQuery/Untitled%2011.png)

### 애니메이션 실습01

- 버튼을 누름으로써 이동하는 객체를 구현해본다
- jquery_05.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

    <style>
        *{
            margin:0;
            padding:0;
        }
        body{
            padding: 20px;
        }
        .btn-wrap{
            margin-bottom : 10px;
        }
        .wrap{
            max-width:600px;
            border : 1px solid black;
        }
        .txt1{
            width:10%;
            text-align: center;
            background-color: aqua;
        }
    </style>
    <script>
        $(function(){
            let txt1=$(".txt1");
            let count = 1;
            $(".btn-wrap button").on("click", function(){
                let ts = $(this);
                if(ts.hasClass("back-button")){
                    count--;
                    
                    if(count < 1){
                        count = 1;
                        return;
                    }
                    txt1.animate({marginLeft:"-=10%"}, 500);
                }
               else{
                    count++;
                    if(count > 10){
                        count = 10;
                        return;
                    }
                    txt1.animate({marginLeft:"+=10%"}, 500);
                }
            });
        });
    </script>
</head>
<body>
    <p class="btn-wrap">
        <button class="back-button">back</button>
        <button class="go-button">go</button>
    </p>
    <div class="wrap">
        <p class="txt1">내용1</p>
    </div>
    
</body>
</html>
```

- 결과
- back에 의해 뒤로, go에 의해 앞으로 이동한다

![Untitled](/images/JS_JQuery/Untitled%2012.png)