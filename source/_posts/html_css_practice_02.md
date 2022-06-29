---
title: "html & css 기초 되집기2"
tags:
  - setting
  - HTML
categories:
  - frontEnd 
  - html & css
author: "minkuen"
date: '2022-06-16'
---


0608 - CSS

### 사전 준비

- 웹 사이트 따라 만들기 : 소스 파일 다운로드
    - 링크 : [http://www.easyspub.co.kr/30_Menu/DataList/PUB](http://www.easyspub.co.kr/30_Menu/DataList/PUB)

![Untitled](/images/html_css_practice_02/Untitled.png)

- 다운로드 받은 파일 압축풀기
- 파일 우클릭 → git bash → code .

### ch03/index.html

- Do it! 웹 사이트 따라 만들기 78p
- 교재 내용대로 작성된 html파일을 열어보자

![Untitled](/images/html_css_practice_02/Untitled%201.png)

- 해당 html에서 Web developer를 이용해 CSS를 제거하면 다음과 같다.

![Untitled](/images/html_css_practice_02/Untitled%202.png)

- 해당 그림의 html파일이다

```css
<!DOCTYPE html>
<html>
<head>
<title>이지스퍼블리싱</title>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, target-densitydpi=medium-dpi">
<!-- 전화, 주소, 이메일 자동 링크 없앨 때 -->
<!--<meta name="format-detection" content="telephone=no, address=no, email=no" />-->
<!-- 기본 포맷 삭제 -->
<!--<meta name="format-detection" content="no" />-->
<meta name="title"  property="og:title" content="이지스퍼블리싱">
<meta name="images" property="og:image" content="./images/link_thumb.jpg">
<meta name="description" property="og:description" content="이지스퍼블리싱">
<meta name="type" property="og:type" content="article">
<script type="text/javascript" src="./js/jquery-3.2.1.min.js"></script>
<script type="text/javascript" src="./js/ui.js"></script>
<link rel="stylesheet" type="text/css" href="./css/ui.css">
</head>
<body>
	<section id="wrap">
		<h1>이지스퍼블리싱</h1>
		<header>
			<!-- alt = 이미지를 읽을 수 없을 때 대응하는 대신 출력 -->
		 	<strong class="logo_box"><img src="./images/mainLogo.png" alt="이지스퍼블리싱"></strong>
		 	<nav>        
		 		<ul>        
					 <!-- 링크를 달기 전의 상태 -->
		 			<li><a href="#">회사소개</a></li>        
		 			<li><a href="#">도서소개</a></li>        
		 			<li><a href="#">FAQ</a></li>        
		 			<li><a href="#">Contact Us</a></li>    
		 		</ul> 
		 	</nav>
		</header> 
		<section id="container">
		  	<section id="menu1" class="content">
		  	 	<h2>회사소개</h2>
		  	 	<div class="conbox"></div>
		  	</section>
		  	<section id="menu2" class="content">
		  	 	<h2>도서소개</h2>
		  	 	<div class="conbox"></div>
		  	</section>
		  	<section id="menu3" class="content">
		  	 	<h2>FAQ</h2>
		  	 	<div class="conbox"></div>
		  	</section>
		  	<section id="menu4" class="content">
		  	 	<h2>Contact Us</h2>
		  	 	<div class="conbox"></div>
		  	</section>
		  </section>    
		  <footer>
		  	  <address>(04003)서울특별시 마포구 잔다리로 109 TEL (02)325-1722 FAX (02)326-1723</address>    
		  	  <p>Copyright(c)2015 이지스퍼블리싱㈜ EasysPublishing Co., Ltd. All Rights Reserved</p> 
		  	  <a href="https://www.facebook.com/easyspub" class="face" title="페이스북으로 이동"></a>    
		  	  <a href="https://twitter.com/easyspub" class="twit" title="트위터로 이동"></a>    
		  	  <a href="https://www.instagram.com/easyspub_book/" class="instar" title="인스타그램으로 이동"></a>
		  </footer> 
	</section>
</body>
</html>
```

- 다음 css 파일을 적용하면 맨 첨음 그림과 같이 출력된다.
- 가상요소에 대한 내용 참고 : 35~37, 92페이지
    - 참고자료 : Do it. 웹 사이트 따라 만들기

```css
@charset "utf-8";
@import url(https://cdn.rawgit.com/theeluwin/NotoSansKR-Hestia/master/stylesheets/NotoSansKR-Hestia.css);

html, body, div, span, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, button, abbr, acronym, address, code, del, 
dfn, em, img, strong, sub, sup, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, 
td, hr{margin:0;padding:0;font-size:100%;box-sizing: border-box;}
body{height:100%;min-height:100%;font-family:'Noto Sans Korean','Malgun Gothic','맑은고딕','돋움',dotum, sans-serif;font-size:16px;color:#737373;line-height:1.5;background:url(../images/content_bg4.png) repeat;}
h1, h2, h3, h4, h5, h6 {font-weight:normal}
ol, ul, li {list-style:none}
table {width:100%; border-collapse:collapse;border-spacing:0}
form, fieldset, iframe {display:block;border:0}
img, button {border:0 none;vertical-align:top;}
hr {height:0; display:none}
i, em, address{font-style:normal}
label, button{cursor:pointer}
blockquote, q {quotes:none}
caption, legend {overflow:hidden;visibility:hidden;position:absolute;width:0;height:0;padding:0;margin:0;font-size:0;text-indent:-100%;white-space:nowrap;z-index:-1}
header, footer, section, article, aside, nav, hgroup, details, menu, figure, figcaption {display:block;box-sizing: border-box;}
input, textarea, select, button {font-family:'Noto Sans Korean','Malgun Gothic','맑은고딕','돋움',dotum, sans-serif;font-size:16px;color:#919090;line-height:1.5;letter-spacing:0;vertical-align:middle; border:none;}
input, textarea {margin:0;padding:0;  background:none; box-sizing:border-box;}
textarea {resize:none}
a {color:#919090;text-decoration:none}
a:link, a:visited {text-decoration:none}
a:hover {text-decoration:none}
.blind{display: none;overflow: hidden;position: absolute;width: 0;height: 0;padding: 0;margin: 0; font-size: 0;line-height: 0; text-indent: -9999em;visibility: hidden;outline: none;z-index: -1;}
html,body{overflow:hidden;height:100%;}

/*layout*/
/* 오른쪽 padding을 180px */
#wrap{width:100%; height:100%; padding-right:180px;}

/* 자식. 보이지 않게 함 */
#wrap > h1{font-size:0;}

/* 자손. 로고의 위치를 절대위치로 지정 */
header .logo_box{position:absolute; right:35px; top:75px;}

/* 절대 위치 지정한 곳에 100px로 이미지 처리 */
header .logo_box img{width:100px;}

/* repeat-y = 검은색 배경에 관여. z-index = 11번째 위치의 높이 */
#wrap header{width:180px; height:100%; position:fixed; right:0px; top:0px; background:url(../images/menu_bg1.png) repeat-y; z-index:11;}
#wrap header nav{width:100%; height:100%;} 

/* flex 이면서 밑으로 나열, 위아래가 같도록 정렬 */
#wrap header nav ul{width:100%; height:100%; display:flex; flex-direction:column; justify-content:center;}

/* margin 은 시계 방향 top, right, bottom, left / ul의 padiing은 .은 적용 안됨 */
#wrap header nav ul li{margin:0px 0px 10px 30px; padding-left:15px; position:relative;} 
#wrap header nav ul li a{font-size:16px; color:#fff; font-weight:600; line-height:30px;}
#wrap header nav ul li:after{content:""; display:block; width:5px; height:5px; border-radius:50%; background:#fff; position:absolute; left:0px; top:13px;}

/* hover(마우스 위에 올라왔을 때) red로 강조함 */
/* on class의 의미는? */
#wrap header nav ul li:hover a,#wrap header nav ul li.on a{color:#ed3140;} 
#wrap header nav ul li:hover:after,#wrap header nav ul li.on:after{background:#ed3140;}
footer{width:180px; position:fixed; right:0px; bottom:0px; padding:0px 20px 30px 20px; font-size:11px; color:#7e7e7e; z-index:12;}
footer address{padding:0px 0px 15px 0px;}

/* transition = 애니메이션의 시간 (4초) */
/* block은 box와 연관된 것 */
footer > a{display:block; width:16px; height:16px; position:absolute; top:-31px; transition:.4s;} 
footer > a.face{background:url(../images/social_b_facebook.png) no-repeat; right:18px;} 
footer > a.face:hover{background:url(../images/social_b_facebook_hover.png) no-repeat;} 
footer > a.twit{background:url(../images/social_b_twitter.png) no-repeat; right:48px;} 
footer > a.twit:hover{background:url(../images/social_b_twitter_hover.png) no-repeat;} 
footer > a.instar{background:url(../images/social_b_instar.png) no-repeat; right:80px;} 
footer > a.instar:hover{background:url(../images/social_b_instar_hover.png) no-repeat;}

/* max-width는 화면 해상도가 1200px이 넘더라도 1200px만 표현, 중앙에 표현 */
/* margin = 0, auto 의미는? --------------------------- */
#container{width:100%; height:100%; position:relative; max-width:1200px; margin:0 auto;} 

/* 4개의 content를 25%로 동일하게 적용 */
#container .content{width:25%; height:100%; position:absolute;} 

/* position이 absolute 이므로 left의 크기가 25%씩 연결되어 붙음 */
/* repeat은 x,y가 모두 적용됨 */
#container #menu1{left:0%; background:url(../images/content_bg1.png) repeat;} 
#container #menu2{left:25%; background:url(../images/content_bg2.png) repeat;} 
#container #menu3{left:50%; background:url(../images/content_bg3.png) repeat;} 
#container #menu4{left:75%; background:url(../images/content_bg4.png) repeat;}

/*가상요소 활용하기*/
#container .content:before,#container .content:after{content:""; display:block; position:absolute;} 
#container .content:before{width:1px; height:100%; background:#000; left:0; top:0; z-index:4;}
#container .content:after{left:30px; top:180px; font-size:25px; font-weight:700; color:#ed3140;}

/* before = 지정한 것을 텍스트 앞에 둔다 */
/* after = 지정한 것을 텍스트 뒤에 둔다 */
#container #menu1:after{content:"회사소개";} 
#container #menu2:after{content:"도서소개";} 
#container #menu3:after{content:"FAQ";} 
#container #menu4:after{content:"Contact Us";}
#container .content .conbox:before{content:""; display:block; position:absolute;} 
#container #menu1 .conbox:before{background:url(../images/main_ico1.png) no-repeat; width:350px; height:260px; right:-10px; top:130px; background-size:100%;} 
#container #menu2 .conbox:before{background:url(../images/main_ico2.png) no-repeat; width:180px; height:470px; right:-30px; top:180px; background-size:100%;} 
#container #menu3 .conbox:before{background:url(../images/main_ico3.png) no-repeat; width:270px; height:310px; right:-60px; top:30px; background-size:100%;} 
#container #menu4 .conbox:before{background:url(../images/main_ico4.png) no-repeat; width:350px; height:400px; right:-170px; top:100px; background-size:100%;}
#container .content h2{opacity:0;}
```

- Reference : Do it! 웹 사이트 따라 만들기
    - [http://www.easyspub.co.kr/30_Menu/DataList/PUB](http://www.easyspub.co.kr/30_Menu/DataList/PUB)