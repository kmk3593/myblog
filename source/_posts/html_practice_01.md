---
title: "html 기초 되집기"
tags:
  - setting
  - HTML
categories:
  - frontEnd 
  - html & css
author: "minkuen"
date: '2022-06-13'
---

# 0607 - HTML

### 경로 설정

- 네이버 화면이 index.html
- 첫 화면이 index.html

![Untitled](/images/html_practice_01/Untitled.png)

## 폴더 구조를 어떻게 할 것인가?

- root 밑에 파일을 다 나열할 수도 있다
- 그러나 이건 별로다
- 권고사항은 index.html에서 버튼을 클릭할때 링크로

# 상대 경로

- 나를 기준으로 상대적으로 다른 폴더나 파일을 찾아간다.
- 절대경로는 root폴더가 기준이 된다. 지금은 HTML폴더

## 부모 폴더 찾기

../  → 부모 폴더로 간다

### 폴더 경로 현황

![Untitled](/images/html_practice_01/Untitled%201.png)

### index.html

![Untitled](/images/html_practice_01/Untitled%202.png)

### notice.html

![Untitled](/images/html_practice_01/Untitled%203.png)

### login.html

![Untitled](/images/html_practice_01/Untitled%204.png)

## 절대 경로

- 모든 파일에서 절대 경로를 사용하면 똑같다.

![Untitled](/images/html_practice_01/Untitled%205.png)

- 절대 경로가 쉬워 보이지만, 나중에 폴더를 바꾸게 되면 더 복잡해진다.
- 따라서, 케바케.
- 보통 절대경로를 쓸지 상대경로를 쓸지는 PM이 결정한다.

![Untitled](/images/html_practice_01/Untitled%206.png)

## 웹문서 작성 1단계  - 콘텐츠 작성하기

- 작성하기 전에 어떻게 생겼는지 확인해보자

![Untitled](/images/html_practice_01/Untitled%207.png)

## web developer 설치

- 구글링 : chrome web store
- chrome web store 검색 : web developer

![Untitled](/images/html_practice_01/Untitled%208.png)

## web developer 사용법

- 화면 우측 상단 ‘퍼즐모양’ 버튼 클릭

![Untitled](/images/html_practice_01/Untitled%209.png)

- Web Developer 선택 후 다음 내용 선택
- CSS → Disable All Styles

![Untitled](/images/html_practice_01/Untitled%2010.png)

- CSS가 제거된 네이버 화면

![Untitled](/images/html_practice_01/Untitled%2011.png)

## 웹문서 작성 2단계 - 콘텐츠 블록의 종류

- 콘텐츠를 작성했다 치고
- head 부분은 거의 표준화가 되서 신경 쓸 게 없다.

- UL

![Untitled](/images/html_practice_01/Untitled%2012.png)

### 입력폼

![Untitled](/images/html_practice_01/Untitled%2013.png)

### 제목 입력

- h1 ~ h6 사용하여 크기 조절 가능

![Untitled](/images/html_practice_01/Untitled%2014.png)

### 목록

- UL : Unordered List (순서가 없는 것에 적합)
- OL : Ordered List (순서가 있는 것에 적합)
- DL : Definition List (데이터 정의하는 것에 적합)
- LI : List Item

![Untitled](/images/html_practice_01/Untitled%2015.png)

### 입력폼

- password 타입을 가지게 되면 보이지 않게 된다.

![Untitled](/images/html_practice_01/Untitled%2016.png)

### 콘텐츠 작성 실습

링크 : [https://www.newlecture.com/](https://www.newlecture.com/)

![Untitled](/images/html_practice_01/Untitled%2017.png)

- 다음과 같이 제작해 보자

![Untitled](/images/html_practice_01/Untitled%2018.png)

## 인풋 검색 상자

- 텍스트 입력 창 생성
- 버튼 생성

![Untitled](/images/html_practice_01/Untitled%2019.png)

## 콤보상자

- 콤보 생성

![Untitled](/images/html_practice_01/Untitled%2020.png)

## 테이블

- 테이블 생성 양식
- border 속성으로 구분 가능
    - border = 0으로 하면 경계선이 사라진다

![Untitled](/images/html_practice_01/Untitled%2021.png)

- tr → table record
- td → table data
- 지금은 직접 넣어줬지만, 나중에는 jsp와 스프링으로 데이터베이스를 끌어오게 된다.

![Untitled](/images/html_practice_01/Untitled%2022.png)

### 웹문서 작성 3단계 - outline 설정하기

- 영역을 구분한다

![Untitled](/images/html_practice_01/Untitled%2023.png)

# CSS

- Cascading Style Sheet
- HTML 문서에 스타일을 입히는 작업이다

![Untitled](/images/html_practice_01/Untitled%2024.png)

### 영역 구분하기

- 코드에서 해당 부분을 header로 구분할 것이다

![Untitled](/images/html_practice_01/Untitled%2025.png)

- <header>  </header> 로 코드를 감싼다.
- 다음과 같이 표시한다.

```html
 	
		<header>
        
    <h1> 뉴렉처 온라인</h1>
    <ul>
        <li>학습가이드</li>
        <li>강좌선택</li>
        <li>answerls</li>
    </ul>
    <input type="text">
    <input type="submit" value="클릭">
    <ul>
        <li>home</li>
        <li>로그인</li>
        <li>회원가입</li>
    </ul>
    <ul>
        <li>마이페이지</li>
        <li>고객센타</li>
    </ul>
    
    </header>
```

- main, footer도 마찬가지로 포장한다
    - <main></main> , <footer> </footer>를 코드의 위아래로 두면 된다.
- 남는 부분은 aside로 포장한다

```html
		<aside>
    <h2>고객센터</h2>
    <h3>고객센터메뉴</h3>
        <ul>
            <nav>
            <li>공지사항</li>
            <li>자주하는 질문</li>
            <li>수강문의</li>
            <li>이벤트</li>
            </nav>
        </ul>
    <h3>협력업체</h3>
    <ul>
        <li>NOTEPUBS</li>
        <li>NAMOOLAB</li>
    </ul>
    </aside>
```

### 섹션

- css로 전환할 때 디자인을 적용하기 위한 사전단계
- 영역구분과 마찬가지로 표시한다.
    - 단, section의 안쪽은 section과 함께 Tab으로 들여쓰기 해준다.

```html
		<header>
        <section>
        <h1> 뉴렉처 온라인</h1>
        <ul>
            <li>학습가이드</li>
            <li>강좌선택</li>
            <li>answerls</li>
        </ul>
        <input type="text">
        <input type="submit" value="클릭">
        <ul>
            <li>home</li>
            <li>로그인</li>
            <li>회원가입</li>
        </ul>
        <ul>
            <li>마이페이지</li>
            <li>고객센타</li>
        </ul>
        </section>
    </header>
```

### 라인 영역 구분

- ul li
- ul li 의 경우, **라인 하나를 통째로 사용**한다

```html
				<ul>
            <li>학습가이드</li>
            <li>강좌선택</li>
            <li>answerls</li>
        </ul>
```

- 해당 코드를 다음과 같이 붙여써보자

```html
				<ul>
            <li>학습가이드</li>li>강좌선택</li><li>answerls</li>
        </ul>
```

- 위 두 코드 모두 다음과 같이 출력된다

![Untitled](/images/html_practice_01/Untitled%2026.png)

- <div>
- <div> 의 경우, **라인의 일부**만 ****사용할 수 있다

```html
		<div>text1</div>
    <div>text1</div>
    <div>text1</div>

    <br>		

		<div>
        <a>열공</a>
        <b>화이팅</b>
        <i>응원합니다.</i>
    </div>
```

- 다음과 같이 붙여써보자

```html
		<div>text1</div>
    <div>text1</div>
    <div>text1</div>

    <br>		

			<div><a>열공</a><b>화이팅</b><i>응원합니다.</i></div>
```

- 위 두 코드의 결과는 동일하다

![Untitled](/images/html_practice_01/Untitled%2027.png)