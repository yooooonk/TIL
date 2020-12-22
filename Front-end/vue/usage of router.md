# 라우터 사용

### 로그인전 페이지 이동

```javascript
import Vue from "vue";
import VueRouter from "vue-router";
import store from "../store";

import Home from "../components/Home.vue";
import Login from "../components/Login.vue";
import Board from "../components/Board.vue";
import Card from "../components/Card.vue";
import NotFound from "../components/NotFound.vue";

Vue.use(VueRouter); // $route로 접근가능

const requireAuth = (to, from, next) => {
  const loginPath = `/login?rPath=${encodeURIComponent(to.path)}`;

  store.getters.isAuth ? next() : next(loginPath);
};

const routes = [
  { path: "/", component: Home, beforeEnter: requireAuth },
  { path: "/login", component: Login },
  {
    path: "/b/:bid",
    component: Board,
    beforeEnter: requireAuth,
    children: [{ path: "c/:cid", component: Card, beforeEnter: requireAuth }],
  },
  { path: "*", component: NotFound },
];

const router = new VueRouter({
  mode: "history",
  routes,
});

export default router;
```

### 인증, role에 따라 페이지이동

```javascript
import Vue from "vue";
import VueRouter from "vue-router";

import LoginRouter from "./index_login";
import DashboardRouter from "./index_dashboard";
import ErrorRouter from "./index_error";

Vue.use(VueRouter);

const requireAuth = () => (from, to, next) => {
  if (from.path.indexOf("ws") === -1) {
    sessionStorage.setItem("currentPage", from.path);
  }

  const { isAuth } = sessionStorage;

  if (isAuth === "true") {
    if(initLogin === 'true'){
        sessionStorage.removeItem("isAuth");
        location.href = "/login";
    }

    if (checkRole(from, to, next)) {
        return next();
    } else {
        return next("/error404");
    }

    next('/login')
}

const checkRole = (...url)=>{
    let rtn = true
    const path = url[0].path;
    const role = sessionStorage.getItem('role')

    if(path.indexOf('/setting')>-1){
        if(role==='ROLE_MANAGER'){
            rtn = false
        }
    }

    return rtn
}

let routes = [
    {path:'/',redirect:'/Home'},
]
routes = routes.concat(LoginRouter);
routes = routes.concat(DashboardRouter);
routes = routes.concat(ErrorRouter);

export default router
```

DashboardRouter

```javascript
const routes = [
  (path: "/dashboard"),
  (name: "dashboard"),
  (component: dashboard),
  (meta: {
    breadcrumb: "대시보드",
  }),
];

export default routes;
```
