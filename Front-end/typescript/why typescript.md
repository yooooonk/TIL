![](https://images.velog.io/images/ouo_yoonk/post/5356b46d-709a-4253-b514-976dd6e84b7f/Why_TypeScript_.png)

# 타입스크립트란?

> TypeScript는 컴파일-타임 타입 검사자가 있는 JavaScript의 런타임입니다.

- 타입스크립트는 자바스크립트에 __타입__ 을 부여한 언어다.
- __정적 타입 검사자__ 로서 프로그램을 실행시키기 전에 값의 종류를 기반으로 프로그램의 오류를 찾는다.
-   자바스크립트 코드의 __런타임 특성__ 을 절대 변화시키지 않는다. 타입스크립트의 컴파일러가 코드 검사를 마치면 타입을 삭제해서 결과적으로 '컴파일된' 코드를 만든다. 즉 코드가 한번 컴파일되면, 결과로 나온 일반 JS 코드에는 타입 정보가 없다.
-   TypeScript는 Javascript의 __상위 레이어__ 다. Javascript의 기능을 제공하면서 그 위에 자체 레이어를 추가한다. 자바스크립트는 원시타입(string, number, object, undefined 등)을 가지고 있지만, 전체 코드베이스에 일관되게 할당되었는지는 미리 확인해주지 않는다. 타입스크립트는 이 레이어로서 동작한다.
- 클래스, 인터페이스, 모듈 등의 강력한 기능을 제공하며, 순수한 __객체 지향 코드__ 를 작성할 수 있다.

## 장점

### 에러의 사전 방지
함수, 컴포넌트 등의 타입을 추론할 수 있어 코드를 실행하지 않아도 IDE 상에서 바로 알 수 있다.
### 코드 가이드 및 자동 완성
자동완성이 굉장히 잘된다. 함수를 사용 할 때 해당 함수가 어떤 파라미터를 필요로 하는지, 그리고 어떤 값을 반환하는지 코드를 따로 열어보지 않아도 알 수 있다.

### 프로그램 부분 간의 더 명확한 통신
리액트 컴포넌트의 경우 해당 컴포넌트를 사용하게 될 때 props에 무엇을 전달해줘야하는지, JSX를 작성하는 과정에서 바로 알 수 있고, 컴포넌트 내부에서도 자신의 props나 state에 어떤 값이 있는지, redux의 store 안에 어떤 상태가 들어있는지 바로 알 수 있다.

## 타입스크립트 프로젝트 시작하기
1. 타입스크립트 파일 생성 및 작성
`.ts` 확장자
``` javascript
// index.ts
function sum(a: number, b: number): number {
  return a + b;
}

sum(10, 20);

```
2. 타입스크립트 설치
`$ npm i typescript -g`
3. 자바스크립트 컴파일
`$ tsc index.ts`
![](https://images.velog.io/images/ouo_yoonk/post/bd6fb56a-0293-4d3b-8f33-d3c629b8922f/image.png)
![](https://images.velog.io/images/ouo_yoonk/post/2fb9f55c-66de-432d-97d8-fba679aa0b6c/image.png)

## 타입스크립트 설정 파일 옵션
`tsconfig.json`

__예시]__
``` javascript
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": true // 암시적으로 선언되었는데 any로 추론되면 에러 발생
  }
}

```

**📑 referece**

-   [인프런 - 타입스크립트 입문(캡틴판교)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)
-   [타입스크립트 - kr](https://typescript-kr.github.io/)