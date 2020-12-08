# 라우팅
- 주소로 식별해 페이지를 이동
- 서버 라우팅 : 주소를 요청할 때마다 화면이 갱신됨 ex]네이버, 구글
- 브라우저 라우팅 : 주소를 요청해도 화면이 갱신되지 않고, 화면에 필요한 데이터만 요청, 서버라우팅보다 효율적으로 화면을 갱신 ex] 구글메일, 트렐로 -- Single Page Application

## 라우터만들기
```javascript
import Vue from 'vue'
import App from './App.vue'

const Login = {template:'<div>Login Page</div>'}

const routes = {
  '/' : App,
  '/login':Login
}

new Vue({
  el: '#app',
  computed:{
    VueComponent(){
      return routes[window.location.pathname]||{
        template:'<div>page not found</div>'
      }
    }
  },
  render(h){ //render: h => h(App)
    return h(this.VueComponent) 
  }
})

```

## 뷰 라우터 사용
1. 라우트 컴포넌트 정의
2. 라우트 정의
3. router 인스턴스 만들기
4. 루트 인스턴스 만들고 앱과 mount시키기
``` javascript
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

// 1. 라우트 컴포넌트 정의
const Login = {template:'<div>Login Page</div>'}
const NotFound = {template:'<div>page not found</div>'}

//2. 라우트 정의
const routes = [
  { path: '/', component: App },
  { path: '/login', component: Login },
  { path: '*', component: NotFound }
]

// 3. router 인스턴스 만들기
const router = new VueRouter({
  mode:'history',
  routes
})

// 4. 루트 인스턴스를 만들고 mounter
new Vue({
  el: '#app',
  router,
  render : h=>h({template:'<router-view></router-view>'})
})

```
## 라우터링크
- 정의 : 라우터 지원 앱에서 사용자 네비게이션을 가능하게하는 컴포넌트 
-`<router-link to="/xx"></router-link>`
- `<a href="..."></a>`와의 차이점?
 - HTML5 히스토리 모드와 해시 모드에서 모두 동일한 방식으로 작동하므로 url 수정이 필요없다
 - 페이지를 다시 리로드하지 않는다

## 동적 라우트 매칭
- 주어진 패턴을 가진 라우트를 동일한 컴포넌트에 매핑해야 하는 경우에 사용
- 여러개도 가능

|패턴|일치하는 패스|$route.params|
|--|--|--|
|/user/:username |/user/evan |	{ username: 'evan' }|
|/user/:username/post/:post_id	| /user/evan/post/123 |	{ username: 'evan', post_id: '123' }|

``` javascript
const User = {
  template: '<div>User</div>'
}

const router = new VueRouter({
  routes: [
    // 동적 세그먼트는 콜론으로 시작합니다.
    { path: '/user/:id', component: User }
  ]
})
```

## 중첩 컴포넌트
- `<route-view>`
``` javascript
const router = new VueRouter({
  routes: [
    // 동적 세그먼트는 콜론으로 시작합니다.
    { path: '/user/:id', component: User, children:[
        {path:'c/:id', component:profile}
    ] }
  ]
})
```
## 네비게이션 가드
- 주로 리다이렉션하거나 췻고하여 네비게이션을 보호하는 데 사용
- router.beforeEach(to, from, next): 전역 가드
- beforeEnter(to, from, next) : 라우트 별 가드
  - to : 라우트, 대상 router 객체로 이동
  - from : 라우트, 현재 라우트로 오기전 라우트
  - next : 함수
    - next() : 파이프라인의 다음 훅으로 이동
    - next(false) : 현재 네비게이션을 중단, 브라우저 url이 변경되면 from 경로의 url로 재설정
    - next('/') 또는 next({path:'/'}) : 다른 위치로 리다이렉션
``` javascript
const requireAuth = (to,from,next)=>{
      const isAuth = localStorage.getItem('token')
      const loginPath = `/login?rPath=${encodeURIComponent(to.path)}`

      isAuth? next():next(loginPath)
}

const routes = [
  { path: '/', component: Home, beforeEnter : requireAuth },  
]


```    

---
__reference__
- [트렐로 개발로 배우는 Vuejs, Vuex,Vue-Router 프론트엔드 실전 기술]
- [vue router](https://router.vuejs.org/kr/guide/#html)