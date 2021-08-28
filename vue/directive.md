# Directive
- v- 접두사가 있는 특수 속성
- 디렉티브 속성은 단인 javaScript 표현식이 됨
- 디렉티브의 역할은 표현식의 값이 변경될 때 사이드이펙트를 반응적으로 DOM에 적용하는 것
- :으로 표시되는 전달인사를 사용할 수 있다

## v-if
- 조건부 렌더링  
- ``` <v-if><v-else-if><v-else>```
- 해당 태그의 하위태그에도 동작
### v-show와의 차이?
- <v-if="false"> : 렌더링 자체가 안됨 
- <v-show="false"> : 렌더링은 되고 display='none'속성으로 화면에 안보이게 처리됨

## v-for
- 리스트 렌더링

### _배열변경 감지_
- push() pop() shitf() unshift() slice() sort() reverse()
- filter() concat() slice() --> 새로운 배열 반환

### _배열번화를 감지 못하는 경우_
- 인덱스로 배열에 있는 항목을 직접 설정하는 경우  
 ex] this.items[index] = '새로운 값
- 배열의 길이를 수정하는 경우
- 동적으로 추가/삭제하는 경우
- __Vue.set__ (obejct, key, value) 
- __vm.$set__(object, key,value)


## v-model
- v-for="아이템명 in array"
- v-for="( item, i ) in list" : i는 list 내의 현재 index 값,0부터 시작



``` html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<div id="app">
 <p v-if="seen">
   이제 나를 볼 수 있어요
 </p>
<ol>
  <li v-for="todo in todos">
    {{todo.text}}    
  </li>
</ol>
<button v-on:click='addTodo'>
  추가
</button>
<input type="text" v-model='message'>
</div>
```
``` js
new Vue({
	el : '#app',
  data:{
  seen:true, //false  
   todos: [
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ],
    message:''
  },
  methods:{
  	addTodo:function(){
    	this.todos.push({text:this.message})
      
    }
  }
  
})
```
----
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- 『Vue.js 첫걸음 - 이지호 지음』
- [버미노트 - 이벤트핸들링](https://beomy.tistory.com/53)