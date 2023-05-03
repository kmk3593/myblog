---
title: "Vue Cli"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-05-03'
---

[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****



[Vue CLI 공식 사이트 링크](https://cli.vuejs.org/)

### CLI란?

- CLI = Command Line Interface

### 설치 방법

- 구글링 : vue cli
- Vue CLI 공식페이지 → Installation → 설치 코드 복사

![Untitled](/images/vue_cli/Untitled.png)

- VSCode → 터미널 → 새 터미널
- 버전 확인

```jsx
// 10 이상인 버전이어야 한다
node -v
// 6 이상인 버전이어야 한다
npm -v
```

- 설치 코드 복사 붙여넣기

```jsx
npm install -g @vue/cli

// 권한이 없다면 다음 코드 실행
sudo npm install -g @vue/cli
```

- 설치에 시간이 걸릴 수 있다. 대기한다.

![Untitled](/images/vue_cli/Untitled%201.png)

### CLI 버전별 차이

- VUE CLI 2.X
    - vue init ‘프로젝트 템플릿 유형’ ‘프로젝트 폴더 위치’
    - vue init webpack-simple ‘프로젝트 폴더 위치’

- VUE CLI 3.X
    - vue create ‘프로젝트 폴더 위치’
    - 더 간단하다

### CLI 사용법

- VSCode → 터미널 → 새 터미널 → Command Prompt 터미널
- 생성 : `vew create [프로젝트 폴더 위치]`

![Untitled](/images/vue_cli/Untitled%202.png)

- Vue CLI 버전 4.5 이상이라면 **Vue 2** 선택한다

![Untitled](/images/vue_cli/Untitled%203.png)

- 생성 성공 시 출력되는 메세지

![Untitled](/images/vue_cli/Untitled%204.png)

- vue-cli 라는 프로젝트가 성공적으로 생성되었다.
- 다음 명령으로 실행시킬 수 있다.

```jsx
$  cd vue-cli
$  npm run serve
```

- 명령 실행 후에 출력되는 주소로 이동

![Untitled](/images/vue_cli/Untitled%205.png)

- 다음과 같이 출력되면 성공

![Untitled](/images/vue_cli/Untitled%206.png)

### CLI로 생성한 프로젝트 폴더 구조 확인 및 main.js 파일 설명

---

- 위 과정을 거치면서 다음과 같이 vue-cli 프로젝트가 생성되었다

![Untitled](/images/vue_cli/Untitled%207.png)

- vue-cli → src → main.js
- vue-cli → src → App.vue
- 참고 자료 : [https://velog.io/@freejia/싱글-파일-컴포넌트-소개-및-App.vue](https://velog.io/@freejia/%EC%8B%B1%EA%B8%80-%ED%8C%8C%EC%9D%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%86%8C%EA%B0%9C-%EB%B0%8F-App.vue)

### Vue 파일 구조

- 한 파일에 HTML , JS, CSS 가 모두 들어있다

```jsx
<template>
    <!-- HTML -->
</template>

<script>
    // Java Script
</script>

<style>
    /* CSS */
</style>
```

### 개발할 때 고려해야 할 점

- VSCord 플러그인 설치
    - **Vue 3 Snippets**
    - Vue 파일에서 ! Tab 과 같은 역할을 한다.
    - `vueinit` 입력하고 `Tab`

- 서버 실행 명령에 의해 출력되는 주소에 App.vue 의 코드가 반영된다
- 코드

```jsx
<template lang="">
    <div>
        app 
    </div>
</template>

<script>
export default { 
    
}
</script>

<style lang="">  
</style>
```

- 결과

![Untitled](/images/vue_cli/Untitled%208.png)

### script의 문자 데이터를 화면에 출력

- 코드

```jsx
<template lang="">
    <div>
        {{ str }}
    </div>
</template>

<script>
export default { 
    data:  function(){
        return{
            str: 'hi'
        }
    }
}
</script>

<style lang="">
</style>
```

- 결과

![Untitled](/images/vue_cli/Untitled%209.png)

### 싱글 컴포넌트 체계에서 컴포넌트 등록하기

---

- components 폴더 하위에 생성해야 한다
- 파일 생성 : AppHeader.vue

- 코드 - AppHeader.vue
- ‘renew’ 라는 이름으로 $emit 한다

```jsx
<template>
    <header>
        <h1>{{ propsdata }}</h1>
        <button v-on:click="sendEvent">send</button>
    </header>
</template>

<script>
export default {
    props: ['propsdata']
    ,methods: {
        sendEvent: function () {
            this.$emit('renew');
        }
    }
}
</script>

<style></style>
```

- 코드 - App.vue
- AppHeader.vue의 $emit을 받아서 renewStr 함수를 실행

```jsx
<template>
    <div>
        <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="str" v-on:renew="renewStr"></app-header>
    </div>
</template>

<script>
// 사용할 컴포넌트를 import 한다
import AppHeader from './components/AppHeader.vue';

export default {
    data: function () {
        return {
            str: 'Header'
        }
    },
    components: {
        'app-header': AppHeader
    },
    methods: {
        renewStr: function () {
            this.str = 'hi';
        }
    }
}
</script>

<style></style>
```

- 결과
- 버튼 클릭 → 문자 Header가 hi로 변경된다

![Untitled](/images/vue_cli/Untitled%2010.png)

[템플릿](https://www.notion.so/b1553500115c428eb93900efb8c4febd)