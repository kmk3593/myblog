---
title: "Vue 인스턴스"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-04-18'
---


[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****

### 인스턴스

- 인스턴스는 Vue로 개발할 때 필수로 생성해야 하는 코드

```jsx
new Vue();
```

- 생성 후에 콘솔 창에서 확인 가능

```jsx
var vm = new Vue();
console.log(vm);
```

- 파일 생성 : instance.html
- 코드 작성

```jsx
<div id="app">
        <!--  -->
    </div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                message: 'hi' 
            }
        });
            
    </script>
```

- 결과

![Untitled](/images/vue_instance/Untitled.png)

### 생성자 함수

- 함수 **이름의 첫 이니셜이 대문자**이다
- 콘솔 창에서 코딩

```jsx
function Person(name, job){
	this.name = name;
	this.job = job;	
}

var p = new Person('josh', 'developer');
```

![Untitled](/images/vue_instance/Untitled%201.png)

- 미리 함수를 정의한다
- 정의된 함수를 언제든 가져다 사용 가능하다
- 이것이 `new Vue()`를 **사용하는 이유**

![Untitled](/images/vue_instance/Untitled%202.png)

### 인스턴스 속성

- 인스턴스에서 사용할 수 있는 속성과 API는 다음과 같다

```jsx
new Vue({
	el: ,
	template: ,
	data: ,
	methods: ,
	created: ,
	watch: ,

});
```

- el : 인스턴스가 그려지는 화면의 시작점 (특정 HTML 태그)
- **template** : 화면에 표시할 요소(HTML, CSS 등)
- data : 뷰의 반응성(Reactivity)가 반영된 데이터 속성
- **methods** : 화면의 동작과 이벤트 로직을 제어하는 메서드
- **created** : 뷰의 라이프 사이클과 관련된 속성
- **watch** : data에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의하는 속성