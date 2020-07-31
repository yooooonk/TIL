# Computed
- 템플릿 문법에서 javascript 표현식을 사용하면 쉽게 원하는 데이터를 DOM에 그릴 수 있지만 복잡한 연산을 템플릿 안에서 하게 되면, 코드를 이해하고, 유지보수하는 것이 어려워짐
- 그래서 복잡한 연산을 할 때는 computed 속성을 사용하는 것이 좋다
- computed 속성도 템플릿에 데이터 바인딩할 수 있다
- computed 속성은 종속대상을 캐싱한다
    - 종석대상이 변경될 떄만 함수 호출
    - 종속대상이 변하지 않는 한 여러번 호출해도 다시 계산하지 않고 캐싱한 결과를 즉시 반환
    - 시간이 많이 걸리는 계산을 할 때, computed를 사용하는 것이 효율적
    - 호출할 때마다 새롭게 계산을 해야하는 경우에는 method를 사용
``` html
<div id='app'>
    <p>{{message}}</p>
    <p>{{reversedMessage}}</p>
    <p>{{reveseMessageMethod()}}</p>
</div>
```

``` javascript
var vm = new Vue({
    el : '#app,
    data : {
        message : '안녕하세요오오오'
    },
    computed:{
        reversedMessage:function(){
            return this.message.split(').reverse().join('')
        }
    },
    methods:{
        reveseMessageMethod : function(){
            return this.message.split(').reverse().join('')
        }
    }
})
```

# Watch
- 데이터가 변경되었을 때 호출하는 콜백함수를 정의하는 속성
- 감시할 데이터를 저장하고 그 데이터가 바뀌면 어떠한 함수를 실행하라는 방식의 명령형 프로그래밍 방식
- 대부분의 경우 computed 속성을 사용하는 것이 더 좋지만, 데이터 변경의 응답으로 비동기식 계산이 필요한 경우나 시간이 많이 소요되는 계산을 해야할 때는 watch를 사용하는 것이 좋다

``` html
<div id='app'>
    <p>{{fullName}}}</p>    
</div>
```

``` javascript
var vm = new Vue({
    el : '#app,
    data : {
        firstName:'foo',
        lastName:'bar',
        fullName:'foo bar'

    },
    watch:{
        firstName:function(val){
            this.fullName = val +  this.lastName;
        },
        lastName:function(val){
            this.fullName = this.firstName + val;
        }
    }
})
```
