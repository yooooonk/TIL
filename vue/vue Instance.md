# Vue Instance
- ```var vm = new Vue({ //option })```
- Vue 인스턴스를 참조하기 위해 종종 vm(ViewVodel의 약자)를 사용
- vm.$속성 으로 접근 가능

## Instance의 속성
``` js
new Vue({
  el: ,
  template: ,
  data: ,
  methods: ,
  created: ,
  watch: ,
});
```
- el :인스턴스가 그려지는 화면의 시작점 (특정 HTML 태그)
- template : 화면에 표시할 요소 (HTML, CSS 등)
- data : 뷰의 반응성(Reactivity)이 반영된 데이터 속성
- methods : 화면의 동작과 이벤트 로직을 제어하는 메서드
- created : 뷰의 라이프 사이클과 관련된 속성
- watch : data에서 정의한 속성이 변화했을 때 추가 동작을 수행할 수 있게 정의하는 속성

## Life Cycle Hook
- 어떤 Vue 인스턴스나 컴포넌트가 생성될 때, 미리 사전에 정의된 몇 단계의 과정을 거치게 됨 -> 라이프사이클(lifecycle)
- Vue 인스턴스가 생성된 후 우리 눈에 보여지고, 사라지기까지의 단계
- 크게 4단계
  - create : 인스턴스 생성
  - mount : 인스턴스를 DOM에 마운트 하는 경우
  - update : 데이터가 변경되어 DOM을 업데이트 하는 경우
  - destroy : 없어지는 과정
- 그 과정에서 사용자 정의 로직을 실행할 수 있는 라이프사이클 훅도 호출됨
- Vue의 세계에서 '컨트롤러'가 없다. 컴포넌트의 사ㅛㅇ자 지정 로직은 이러한 라이프사이클 훅으로 분할된다

### beforeCreate
- 가장 먼저 실행됨
- Vue 인스턴스가 초기화 된 직후, 인스턴스가 생성되기 전에 호출
- 컴포넌트가 DOM에 추가되기도 전 -> this.$el에 접근 불가
- data, event, watcher에도 접근하기 전 -> data, methods에도 접근불가

### created
- 인스턴스가 생성된 후에 호출
- data를 반응형으로 추적할 수 있게 되고, computed, methods, watch 등이 활성화되어 접근이 가능해짐
- 아직까지 DOM에는 추가되지 않은 상태
- data에 직접 접근이 가능하기 때문에, 컴퓨넌트 초기에 외부에서 받아온 값들로 data를 셋팅해야 하거나 이벤트 리스너를 선언해야 한다면 이 단계에 하는 것이 적절하다

### beforeMount
- DOM에 부착하기 전
- 이 단계 전에서 템플릿이 있는지 없는지 확인한 후 템플릿을 렌더링 한 상태이므로, 가상 DOM이 생성되어 있으나 실제 DOM에 부착되지는 않은 상태

### mounted
- 일반적으로 가장 많이 사용함
- 가상 DOM의 내용이 실제 DOM에 부착된 후 실행됨
- this.$e, $data, $computed, $methods, $watch 등 모든 요소에 접근 가능
- 부모 컴포넌트의 mounted훅은 항상 자식 컴포넌트의 mounted훅 실행 이후에 실행됨
- this.$nextTick : 모든 화면이 렌더링 된 이후에 실행되므로 마운트 된 상태를 보장할 수 있다

### beforeUpdate
- 컴포넌트에서 사용하는 data의 값이 변해서, DOM에도 그 변화를 적용시켜야 할 때
- 변한 값을 이용해 가상 DOM을 렌더링하기 전이지만, 이 값을 이용해 작업은 가능.
- 이 훅에서 값들을 추가적으로 변화시키더라도 랜더링을 추가로 호출하지는 않는다

### updated
- 가상 DOM을 렌더링 하고 실제 DOM이 변경된 이후에 호출됨
- 변경된 data가 DOM에도 적용된 상태.
- 변경된 값들을 DOM을 이용해 접근하고 싶다면, updated훅이 가장 적절하다
- 이 훅에서 data를 변경하는 것은 무한 루프를 일으킬 수 있으므로 이 훅에서는 데이터를 직접 바꾸어서는 안됨
- mounted훅과 마찬가지로, this.$nextTick을 이용해, 모든 화면이 업데이트 된 이후의 상태를 보장할 수 있다.

### beforeDestroy
- 인스턴스가 제거되기 전
- 인스턴스는 완전하게 작동하므로 모든 요소에 접근 가능
- 인스턴스가 사라지기 전에 해야할 일을 하면 됨 ex] 이벤트 리스너 해제

### destroyed
- 인스턴스가 제거된 후
- 해체가 끝난 이후이기 때문에 인스턴스의 속성에 접근할 수 없다
- 하위 Vue 인스턴스 역시 삭제

---
- [배동훈 - vue.js입문 초보 실전 웹앱 개발-1부](https://www.inflearn.com/course/real-%EC%9B%B9%EC%95%B1-%EA%B0%9C%EB%B0%9C-vuejs-1%EB%B6%80)
- [Cracking vue](https://joshua1988.github.io/vue-camp/vue/instance.html#%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%EC%83%9D%EC%84%B1)
- [vue guide](https://kr.vuejs.org/v2/guide/instance.htmls)
- [재그지그 개발블로그](https://wormwlrm.github.io/2018/12/29/Understanding-Vue-Lifecycle-hooks.html)