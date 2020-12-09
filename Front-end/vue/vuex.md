# Vuex

- Vuex는 Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리
- 애플리케이션의 **모든 컴포넌트에 대한 중앙집중식 저장소** 역할을 하여 예측 가능한 방식으로 상태를 변경할 수 있다
- 단방향 데이터흐름
  - State : 앱을 작동하는 원본 소스
  - View : 상태의 선언적 매핑
  - Action : view에서 사용자 입력에 대해 반응적으로 상태를 바꾸는 방법
- 하위 컴포넌트는 상위컴포넌트로 emit, 상위컴포넌트는 하위 컴포넌트로 props를 통해 데이터를 전달해줌 -- 컴포넌트 중첩관계가 복잡해질수록 복잡해짐 --> 중앙저장소에서 관리
  ![vuex](https://github.com/yooooonk/TIL/blob/master/img/vuex.PNG)
  > npm i vuex

```javascript
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

const store = new Vuex.Store({
  state: {
    //상태
    count: false,
  },
});

export default store;
```

```javascript
import Vue from "vue";
import router from "./router";

import App from "./App.vue";
import store from "./store";

new Vue({
  el: "#app",
  router,
  store,
  render: (h) => h(App),
});
```

## 상태 State

- Vuex는 **단일 상태 트리** 를 사용한다. 이 단일 객체는 모든 애플리케이션 수준의 상태를 포함하여 원본 소스 역할을 한다
- 각 애플리케이션마다 하나의 저장소만 갖게 된다는 것을 의미
- **`mapState`**: compouted 속성에 추가. 컴포넌트가 여러 저장소 상태 속성이냐 getter를 사용해야하는 경우 계산된 속성을 모두 선언하면 반복적이고 장황해진다. 이를 처리하기 위해 계산된 getter 함수를 생성하는 mapState 헬퍼를 사용하여 키 입력을 줄일 수 있다

```javascript
computed: {
    ...mapState(["count"])
  }
  // 바로 count 사용가능
```

## Getters

```javascript
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: "...", done: true },
      { id: 2, text: "...", done: false },
    ],
  },
  getters: {
    doneTodos: (state) => {
      return state.todos.filter((todo) => todo.done);
    },
  },
});
```

- 저장소 상태를 기반하는 상태값을 가져올 때
- 첫 번째 전달인자로 상태를 받는다
- compouted 속성에 `mapGetters` 헬퍼 사용

## 변이 Mutation

```javascript
const store = new Vuex.Store({
  state: {
    //상태
    count: false,
  },
  mutations: {
    increment(state) {
      //상태변이
      state.count++;
    },
    increment2(state, m) {
      state.count += m;
    },
    increment3(state, payload) {
      state.count += payload.amount;
    },
  },
});
```

```javascript
store.commit("increment");
store.commit("increment2", 10);
store.commit({ type: "increment", amount: 10 });
```

- Vuex 저장소에서 실제로 상태를 변경하는 유일한 방법은 변이하는 것
- 핸드러 함수는 실제 상태를 수정하는 곳이며 첫번째 전달인자로 state, 두번째 인자로 payload를 받는다
- 변이 핸드러를 호출하려면 `stotre.commit('handler'{,payload})` 호출 또는 객체 스타일 `store.commit({type:'increment3', amount:10})`
- 변이 타입에 상수를 사용하는 것이 일반패턴
- 변이는 무조건 동기적이어야 한다 - action
- **`mapMutations`**

```javascript
methods:{
    ...mapMutations(["increment"])
}//increment()로 사용가능
```

## 액션

```javascript
const store = new Vuex.Store({
  state: {
    count: 0,
  },
  mutations: {
    increment(state) {
      state.count++;
    },
  },
  actions: {
    increment(context) {
      context.commit("increment");
    },
    incrementAsync({ commit }) {
      setTimeout(() => {
        commit("increment");
      }, 1000);
    },
  },
});
```

- 상태를 직접 변이시키는 것이 아니고 변이를 커밋을 함
- 작업에는 임의의 _비동기 작업_ 이 포함될 수 있다

- `store.dispatch`를 사용

```
├── index.html
├── main.js
├── api
│   └── ... # API 요청을 위한 추상화를 포함합니다.
├── components
│   ├── App.vue
│   └── ...
└── store
    ├── index.js          # 모듈을 조합하고 저장소를 내보내는 곳 입니다.
    ├── actions.js        # 루트 액션
    ├── mutations.js      # 루트 변이
    └── modules
        ├── cart.js       # cart 모듈
        └── products.js   # products 모듈
```

---

**reference**

- [Vuex](https://vuex.vuejs.org/kr/)
