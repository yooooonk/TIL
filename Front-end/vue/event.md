# 이벤트 핸들링
- v-on(ex:v-on:click = @click) 디렉티브는 이벤트 리스너
- DOM 이벤트가 발생하는지 들고 있다가 이벤트가 발생했을 때 javscript를 실행
- 메소드 이벤트 핸들러 : 대부분의 이벤트 핸들러 로직은 복잡하기 때문에 v-on에 javascript로 넘겨주기 어려움   
-> methods의 함수를 넘겨주는 형태로 구현
- 인라인 메소드 핸들러 : 메소드 이름을 v-on에 직접 바인딩 하는 대신 인라인 javascript를 사용하여 methods의 함수를 호출할 수 있음
- __$event__ 라는 인자를 methods의 함수에 넘겨주어 DOM 이벤트 객체를 사용할 수 있다

``` html
<div id='app'>
    <button v-on:click='greet'>GREET</button>
    <button v-on:click='say(hi,$event)'>GREET2</button>
</div>
```

```
var vm = new Vue({
    el:'#app',
    data : {
        message : '안녕하세요'
    }
    methods:{
        greet : function(e){
            alert(this.message)
        }, 
        say : function(message,event){
            laert(message + event.target)
        }
    }
})
```

## 이벤트 수식어
- 네이티브 이벤트 객체에는 엘리먼트의 기본 동작을 취소하거나 이벤트 버블링이 발생하지 않도록 설정할 수 있다
- v-on:이벤트이름.수식어 ex]v-on:click.stop='xx'
- vue.js는 이벤트 리스너에게 DOM에서 발생하는 네이티브 이벤트 객체를 전달함.  
그런데 네이티브 이벤트 객체는 간혹 실제 이벤트가 발생한 엘리먼트의 상위 엘리먼트에도 타겟 엘리먼트와 같은 이벤트를 발생시키는 이벤트 버블링이 발생
- 이벤트 버블링 : 이벤트를 발생시킬 때 타깃 엘리먼트에서 발생한 이벤트를 전파하는 것
- 종류
    - .stop : 상위 엘리먼트로 이벤트가 전파되지 않도록
    - .prevent : 기본동작(하이퍼링크, submit 해당)을 막고 사용자가 원하는 동작을 실행할 때
    - .capture : 타깃 엘리먼트에서 발생한 이벤트를 상위 엘리먼트에서 먼저 처리해야할 때 사용
    - .self : 타겟 엘리먼트에서 직접 발생한 이벤트만 처리
    - .once : 이벤트 리스너를 처음 한번만 실행

## 키수식어
- keyup, keydown, keypress 이벤트에 반응
- .enter .tab .esc .space

## 시스템 수식어키
- .alt .ctrl .exact
    
----
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- 『Vue.js 첫걸음 - 이지호 지음』