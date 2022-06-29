---
title: "html & css 기초 되집기"
tags:
  - setting
  - HTML
categories:
  - frontEnd 
  - html & css
author: "minkuen"
date: '2022-06-14'
---

``
0607 - CSS

### 작업 시작

- VSCord에서 파일을 생성
- ! + Tab
- 코드를 작성

## 스타일 시트 적용

### 스타일 지정방식 1

- 다음과 같은 방식으로 정한다.

```html
<h1 style="color: blue;font: size 5px;">메인메뉴</h1>
```

- 적용된 후의 출력이다

![Untitled](/images/html_css_practice_01/Untitled.png)

### 스타일 지정방식 2

- 다음과 같이 설정한다.
- h1 태그를 설정했으므로 h1으로 출력되는 글은 모두 blue로 나타난다.

```html
<style>
        h1{
            color: blue;
            font-size: 5px;
        }
    </style>
</head>
<body>
    <h1>메인메뉴</h1>
    <ul>
        <li>HTML </li>
        <li>CSS </li>
        <li>JAVA </li> 
    </ul>

</body>
</html>
```

### 스타일 지정방식 3

- style.css 파일

```html
h1{
    color: red;
    font-size: 15px;
}
li{
    background-color: blue;
}
```

- 사용할 css파일의 경로를 지정한다.

```html
<title>Document</title>
    <link href="./css/style.css" type="text/css" rel="stylesheet">

</head>
<body>
    <h1>메인메뉴</h1>
    <ul>
        <li>HTML </li>
        <li>CSS </li>
        <li>JAVA </li> 
    </ul>

</body>
</html>
```

- 다음과 같이 출력된다

![Untitled](/images/html_css_practice_01/Untitled%201.png)

### 선택자 (Selector)

- 스타일 적용에 관한 우선순위를 결정한다

- tag 기준
    - tag명 = 가장 낮음
- class 기준
    - .tag명 = 높은
- id 기준
    - #tag명 = 가장 높음

![Untitled](/images/html_css_practice_01/Untitled%202.png)

- **우선순위**
    - ID > 속성[id] >  속성[class] > class > tag

![Untitled](/images/html_css_practice_01/Untitled%203.png)

- 선택자 : HTML내의 Tag를 선택하는 것 (Tag = Element)
- 선택자는 Basic Selector와 Combinator로 구분됨.
- 자손 : ul li
- 자식 : ul>li

![Untitled](/images/html_css_practice_01/Untitled%204.png)

- 형제
- ol + ul
- ol 다음에 있는 태그를 대상으로 적용 = ol’s next

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        ol+ul{
            background-color: yellow;
        }
    </style>
</head>
<body>
    <section id="main">

        <ul>
            <li>CSS4</li>
            <li>CSS5</li>
        </ul>
        <ol>
            <li>HTML4</li>
            <li>HTML5</li>
        </ol>
        <ul>
            <li>AJAX</li>
            <li>JAVASCRIPT</li>
        </ul>
    </section>
</body>
</html>
```

![Untitled](/images/html_css_practice_01/Untitled%205.png)

### Color

- 프론트엔드에서 중요한 것은 색이다.

![Untitled](/images/html_css_practice_01/Untitled%206.png)

- 다음 코드와 같이 rgb값을 조절해 색을 나타낼 수 있다.

```html
background-color: rgba(170, 125, 228, 0.288);
```

### 박스

- Contents가 차지하는 위치의 표현방법
- **padding** = contents와 border 간의 여백
- **border** = 경계선
- **margin** = 이웃 엘리먼트간의 경계

![Untitled](/images/html_css_practice_01/Untitled%207.png)

- 다음과 같이 코딩해보자
- padding = 여백 설정

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        p{
            border: red solid 1px;
            width: 400px;
            height: 300px;

            /* 시계방향 */
            padding-top: 10px;
            padding-right: 20px;
            padding-bottom: 30px;
            padding-left: 40px;

            /* 모든 padding이 동일*/
            /* padding: 10px;
            margin: 10px; */
        }
    </style>
</head>
<body>
    <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus perspiciatis, atque harum dolore blanditiis delectus. Dolores suscipit, neque nobis totam molestiae amet veniam ratione ullam debitis! Laboriosam saepe possimus fuga.
    </p>
    <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus perspiciatis, atque harum dolore blanditiis delectus. Dolores suscipit, neque nobis totam molestiae amet veniam ratione ullam debitis! Laboriosam saepe possimus fuga.
    </p>
</body>
</html>
```

- 다음과 같이 box 적용된다

![Untitled](/images/html_css_practice_01/Untitled%208.png)

### Box 모델 주의사항

- 마진겹침

![Untitled](/images/html_css_practice_01/Untitled%209.png)

- 다음 코드를 작성해보자

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div{
            width:900px;
            margin: 10px;
        }
        #small{
            border: 10px solid black;
        }
        #large{
            border: 30px solid black;
        }
    </style>
</head>
<body>
    <div id="small">휴먼교육센터1</div>
    <div id="large">휴먼교육센터2</div>
</body>
</html>
```

![Untitled](/images/html_css_practice_01/Untitled%2010.png)

### Position

- 위치 조정 가능

![Untitled](/images/html_css_practice_01/Untitled%2011.png)

- relative를 사용하면 다음과 같다

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
       div{
           border:1px solid gray;
           margin:10px;
           
           /* 생략가능
           position:static; */
           position:relative;
       }
       #me{
           left:100px;
           top:100px;
       }

    </style>
</head>
<body>
    <div>휴먼교육센터</div>
    <div id="parent">present
        <div id="me">child</div>
    </div>

</body>
</html>
```

- static과 달리 child 가 밖으로 나간다

![Untitled](/images/html_css_practice_01/Untitled%2012.png)

- static
- relative
- absolute
- fixed

![Untitled](/images/html_css_practice_01/Untitled%2013.png)

### 레이아웃

- layout 생성 순서

![Untitled](/images/html_css_practice_01/Untitled%2014.png)

### 플랙스

- layout 생성에 사용한다
- Container = 행
- item = 행 내의 세부 layout

![Untitled](/images/html_css_practice_01/Untitled%2015.png)

- flex를 사용해본다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .container{
            background-color: yellow;
            display: flex
        }
        .item{
            background-color: green;
            border: 1px solid black;
        }

    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
    
</body>
</html>
```

- row 속성 사용 : 행 방향으로 전개된다

![Untitled](/images/html_css_practice_01/Untitled%2016.png)

- 여러 속성을 사용해보자
- 참고 자료
    - [https://codepen.io/enxaneta/pen/adLPwv](https://codepen.io/enxaneta/pen/adLPwv)

![Untitled](/images/html_css_practice_01/Untitled%2017.png)

### Holy Grail Layout

- 다음과 같이 구성하는 layout이다

![Untitled](/images/html_css_practice_01/Untitled%2018.png)

- 직접 사용해보자

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #container{
            display:flex;
            flex-direction: column;
        }
        header{
            border-bottom: 1px solid grey;
            padding: left 20px;
        }
        footer{
            border-top: 1px solid gray;
            padding-left: 20px;
        }
        .content{
            display:flex;
            flex-direction: row;
        }
        .content nav {
            border-right: 1px solid grey;
        }
        .content aside {
            border-left: 1px solid grey;
        }
        nav, aside{
            flex-basis:150px;
            flex-shrink: 0;
        }
        main{
            padding:10px;
        }

    </style>
</head>
<body>
    <div id="container">
        <header>
            <h1>휴먼교육센터</h1>
        </header>
        <section class="content">
            <nav>
                <li>학원소개</li>
                <li>과정소개</li>
                <li>게시판</li>
            </nav>
            <main>
                Lorem ipsum dolor sit amet consectetur, adipisicing elit. Nulla ea consectetur eos in labore. Laboriosam, recusandae perspiciatis quidem veniam eveniet quas, porro perferendis corrupti expedita deserunt quam aliquam, doloribus fugit.
                Labore quam delectus sed quia eius quibusdam quos eaque animi harum pariatur dolore consectetur nam excepturi molestias maxime cumque ducimus necessitatibus corporis beatae natus possimus est officia, ipsam deserunt! Inventore.
            </main>
            <aside>
                AD = 광고
            </aside>
        </section>
        <footer>
            <a href="http://www.human.or.kr">홈페이지</a>
        </footer>
    </div>
</body>
</html>
```

- 결과는 다음과 같다

![Untitled](/images/html_css_practice_01/Untitled%2019.png)