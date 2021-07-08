![](https://images.velog.io/images/ouo_yoonk/post/99e3e6ed-4ef3-4e09-b75d-1cb85f6b55bc/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C_%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD%EC%9D%98_%EC%9D%B4%ED%95%B4%EC%99%80_%EC%8B%A4%EC%8A%B5%5B%EA%B9%80%EC%A0%95%ED%99%98%EB%8B%98%5D__n_-_ESLint.png)

# ESLint

> 소스 코드를 분석하여 프로그램 오류, 버그, 스타일 오류, 의심스러운 구조체에 표시(flag)를 달아놓기 위한 도구들을 가리킨다 - 위키백과(린트)

- 린트는 코드의 가독성을 높인다.
- 동적 언어의 특성인 런타임 버그를 예방하는 역할을 한다.

ESLint는 ECMAScript 코드에서 문제점을 검사하고 더 나은 코드로 정정하는 린트 도구 중 하나다. 코드의 가독성을 높이고 잠재적인 오류와 버그를 제거해 단단한 코드를 만드는 것이 목적이다.

- 포맷팅 : 일관된 코드 스타일을 유지해 가독성을 높인다 - 들여쓰기 규칙, 코드 라인의 최대 너비 규칙
- 코드품질 : 어플리케이션의 잠재적인 오류나 버그를 예방 - 사용하지 않는 변수 쓰지 않기, 글로벌 스코프 함부로 다루지 않기

## 설치 및 사용법

- 설치
- 설정파일 : .eslintrc.js
- rules : [eslint Rules](https://eslint.org/docs/rules/)
- **Extensible Config** : 규직을 미리 정해 놓은 것. extends 설정에 추가해서 사용한다. ex] eslint - recommended

```
$ npm i -D eslint
```

**.eslintrc.js**

```javascript
module.exports = {
  extends: ['eslint:recommended']
  // rules:{
  //     "no-unexpected-nultiline:"error"
  // }
};
```

## Rules

---

**&#128209; reference**

- [김정환 - 프론트엔드 개발환경의 이해:ESLint](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)
- [위키백과 - 린트]
