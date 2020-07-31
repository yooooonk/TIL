# 폼입력 바인딩
- __v-model__ 로 양방향 바인딩이 가능
- 초기 value와 checked, selected 속성을 무시함

```html
<div id='app'>
    <input v-model='message'>
    <textarea v-model='message'></textarea>
    <p> 메시지 {{message}} </p>

    <input type='checkbox' v-model='checked'>

    <input type='checkbox' value='빨강' v-model='checkedColor'><label for='red'>RED</label>
    <input type='checkbox' value='노랑' v-model='checkedColor'><label for='yellow'>YELLOW</label>
    <input type='checkbox' value='파랑' v-model='checkedColor'><label for='blue'>BLUE</label>
    <span>선택한 색깔 : {{checkedColor}} </span>

    <select v-model='selected'>
        <option>a</option>
        <option>b</option>
        <option>c</option>
    </select>
    <span>선택한 것 : {{selected}} </span>
    
</div>
```

``` javascript
var vm = new Vue({
    el:'#app',
    data : {
        message : '안녕하세요',
        checked : true,
        checkedColor : [],
        selected : []
    }

})
```
---
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- 처음시작하는 Vue.js