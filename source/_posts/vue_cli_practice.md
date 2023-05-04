---
title: "Vue Cli 실습"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-05-04'
---

[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****


- 기존의 서버가 실행되고 있다면 종료 : `Ctrl + c`
- 터미널을 새로 연다 → command prompt  터미널
- 프로젝트 생성 : `vue create vue-form`
- 옵션 : vue2 선택

- 경로 이동 : `cd vue-form`
- 서버 실행 : `npm run serve`
- 출력된 주소로 이동한다

- 생성된 프로젝트 확인
- HelloWorld.vue 제거
- App.vue에서 코드 작성
    - 첫 생성 상태의 코드 삭제
    - 기본 코드 생성 : `vueinit Tab`

- 기본 틀 생성
- 코드 - App.vue

```jsx
<template lang="">
  <form action="">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text">
    </div>

    <div>
      <label for="password">pw: </label>
      <input id="password" type="password">
    </div>

    <button>login</button>

  </form>
</template>
<script>
export default {
  
}
</script>
<style lang="">
  
</style>
```

- 화면

![Untitled](/images/vue_cli_practice/Untitled.png)

- 입력 창과 컴포넌트에 같은 값이 담기도록 연결한다
    - 태그 출력 부에 `v-model` 사용
    - JS 부에 함수 생성

```jsx
<label for="username">id: </label>
<input id="username" type="text" v-model="username">

...
...

<script>
export default {
  data: function(){
    return {
      username: ''
      , password: ''
    }
  }
  
}
</script>
```

- 입력한 값과 같은 값이 컴포넌트에 담긴다

![Untitled](/images/vue_cli_practice/Untitled%201.png)

- login 버튼 클릭 → 두 입력 창의 값을 들고 오게 해야 한다
- 버튼에 type=”submit” 추가
- 함수 추가

```jsx
<button type="submit">login</button>

... 
...
...

, methods:{
      submitForm: function(event){
        // 버튼 클릭시 새로 고침 되는 것을 막는다
        event.preventDefault();
        console.log(this.username, this.password);
      }
  }
```

- 잠시 서버 종료 : `Ctrl + c`
- axios 다운로드 : `npm i axios`

![Untitled](/images/vue_cli_practice/Untitled%202.png)

- axios import :  `import axios from ‘axios’;`
- 전체 코드

```jsx
<template>
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">id: </label>
      <input id="username" type="text" v-model="username">
    </div>
    <div>
      <label for="password">pw: </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">login</button>
  </form>
</template>

<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      username: ''
      , password: ''
    }
  },
  methods: {
    submitForm: function () {
      // 새로고침을 막는 명령어
      // event.preventDefault();
      console.log(this.username, this.password);
      var url = 'https://jsonplaceholder.typicode.com/users';
      var data = {
        username: this.username,
        password: this.password
      }
      axios.post(url, data)
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  }
}
</script>

<style></style>
```

- 결과
- 입력한 값이 버튼 클릭과 동시에 넘어감을 확인

![Untitled](/images/vue_cli_practice/Untitled%203.png)