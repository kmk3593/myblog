---
title: "Vue 라우터"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-04-22'
---

[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****

### 뷰 라우터

- 뷰 라이브러를 이용하여 **싱글 페이지 에플리케이션을 구현**할 때 사용하는 라이브러리

### **싱글 페이지 에플리케이션**

- 싱글 페이지 애플리케이션은 서버로부터 완전한 새로운 페이지를 불러오지 않는다
- **현재의 페이지를 동적으로 다시 작성**함으로써 **사용자와 소통**하는 웹 애플리케이션이나 **웹사이트**를 말한다

### 뷰 라우터 사용법

- 구글링 : vue router
- 최상단 검색 결과 클릭 → installation
- 링크 복사하기
    - **[https://unpkg.com/vue-router@4](https://unpkg.com/vue-router@4.0.15/dist/vue-router.global.js)**

![Untitled](/images/vue_router/Untitled.png)

- 파일 작성 : router.html
    - Vue.js 가 위
    - Vue router가 아래
    - 순서가 중요하다!

```jsx
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
```

- 코드

```jsx
<div id="app"></div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
    <script>
        var routerOne = new **VueRouter**({

        });

        new Vue({
            el: '#app'
            , **router**: routerOne
        });

    </script>
```

- 결과
- router 확인 가능

![Untitled](/images/vue_router/Untitled%201.png)

### Router 속성

---

- **routes** : 페이지의 라우팅 정보. 배열 형태로 담긴다

```jsx
var routerOne = new VueRouter({
            // 페이지의 라우팅 정보
            routes : [
                // 로그인 페이지 정보
                {
                    // 페이지의 url
                    path: '/login'
                    // 해당 url에서 표시될 컴포넌트
                    , component: LoginComponent
                }
                // 메인 페이지 정보
                , {
                    path: '/main'
                    , component: MainComponent
                }
            ]

        });
```

- 코드
- **router-view** 라는 **설정되어 있는 태그를 사용**하는 듯하다

```jsx
<div id="app">
        <router-view></router-view>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
    <script>
        var LoginComponent ={
            template : '<div>login</div>'
        } 

        var MainComponent ={
            template : '<div>main</div>'
        }

        var routerOne = new VueRouter({
            // 페이지의 라우팅 정보
            routes : [
                // 로그인 페이지 정보
                {
                    // 페이지의 url
                    path: '/login'
                    // 해당 url에서 표시될 컴포넌트
                    , component: LoginComponent
                }
                // 메인 페이지 정보
                , {
                    path: '/main'
                    , component: MainComponent
                }
            ]

        });

        new Vue({
            el: '#app'
            , router: routerOne
        });

    </script>
```

- 결과
- 주소 창에 입력해줘야 한다
    - login
    - main

![Untitled](/images/vue_router/Untitled%202.png)

### 라우터 링크

---

- 링크로 사용하는 라우터
- 코드
    - 위 코드에서 <div> 태그 부분만 변경한다
    - router-view 와 같이 **설정되어 있는 고유의 태그**인 **router-link** 사용한다

```jsx
<div id="app">
    <div>
         <!-- <a href="" ...> 로 쓰는 앵커 태그와 같은 역할  -->
        <router-link to="/login">Login</router-link>
        <router-link to="/main">Main</router-link>
    </div>
    <router-view></router-view>
</div>
```

### 참고자료

- 설치 및 라우터 요약 : [https://joshua1988.github.io/vue-camp/vue/router.html#뷰-라우터-설치](https://joshua1988.github.io/vue-camp/vue/router.html#%E1%84%87%E1%85%B2-%E1%84%85%E1%85%A1%E1%84%8B%E1%85%AE%E1%84%90%E1%85%A5-%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5)
- 뷰 라우터 공식 문서 : [https://v3.router.vuejs.org/](https://v3.router.vuejs.org/)
- • Vue.js와 Vue Router CDN 코드

```jsx
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router@3.5.3/dist/vue-router.js"></script>
```

- 중급 과정 - 네비게이션 가드
    - [https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/)