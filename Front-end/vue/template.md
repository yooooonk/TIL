# Template 문법

## 텍스트 보간법
- vue instance의 data 내에서 선언한 변수?를 머스태쉬 태그 {{ }}를 이용해서 출력할 수 있다
- 모든 데이터 바인딩 내에서 JavaScript 표현식의 모든 기능을 지원
- 조건문은 삼항연산자를 사용해야함

## v-bind
- HTML 태그의 속성 값을 인스턴스 내의 data 값으로 사용해야 하는 경우
- <태그 v-bind:속성='데이터 값'> 또는 <태그 :속성='데이터 값'>
- v-bind를 생략해 : 만 사용 가능  
ex]``` <img v-bind:src='사진1.jpg'>
 <img :src='사진1.jpg'>```
``` js
new Vue({
	el : '#app',
  data:{
  	message : "Hello Vue"
  },
  methods:{
  	reversMessage:function(){
    	this.message = this.message.split('').reverse().join('');
    }
  }
  
})
```
```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<div id="app">
 <p>
   {{message}}
    <button v-on:click='reversMessage'>
   메세지 뒤집기
 </button>
 </p>

 <span v-bind:title='message'>
     동적으로 바인딩 된 title
 </span>
</div>
```
---
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- [velopert](https://velopert.com/3095)
- [vue guide](https://kr.vuejs.org/v2/guide/instance.htmls)