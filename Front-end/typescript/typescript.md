![](https://images.velog.io/images/ouo_yoonk/post/95d08d16-336c-4cde-a573-f264693d328f/Typescript%F0%9F%8C%8A.png)

# 💡Typescript?

![](https://blog.kakaocdn.net/dn/loJt8/btqBtYf8x6A/dXGtYMhcdC8KgIVYH6DXV0/img.png)

Microsoft에서 개발하고 유지/관리하는 오픈소스. 일반 자바스크립트로 컴파일되는 자바스크립트 상위호환으로 2012년 10월에 처음 릴리스 되었다.

자바스크립트는 타입 시스템이 없는 동적 프로그래밍 언어(weakly styped)로 특정 타입으로 변수를 선언한 다음에도 다른 타입의 값을 가질 수 있다. 비교적 유연하게 개발할 수 있는 환경을 제공하지만, 런타임 환경에서 쉽게 에러가 발생할 수 있다.

타입스크립트는 이러한 자바스크립트에 강한 타입 시스템을 적용해 대부분의 에러를 컴파일 환경에서 코드를 입력하는 동안 체크할 수 있다.

## 사용법

타입스크립트는 `.js` 확장자를 가진 파일로 작성할 수 있고, 작성 후 타입스크립트 컴파일러를 통해 자바스크립트 파일로 컴파일하여 사용하게 된다.

## 장점

### 자동완성 타입확인 가능

Typescript를 사용하면 자동완성이 굉장히 잘된다. 함수를 사용 할 때 해당 함수가 어떤 파라미터를 필요로 하는지, 그리고 어떤 값을 반환하는지 코드를 따로 열어보지 않아도 알 수 있다.

리액트 컴포넌트의 경우 해당 컴포넌트를 사용하게 될 때 props에 무엇을 전달해줘야하는지, JSX를 작성하는 과정에서 바로 알 수 있고, 컴포넌트 내부에서도 자신의 props나 state에 어떤 값이 있는지, redux의 store 안에 어떤 상태가 들어있는지 바로 알 수 있다.

### 실수방지

함수, 컴포넌트 등의 타입을 추론할 수 있어 코드를 실행하지 않아도 IDE 상에서 바로 알 수 있다.

## 타입스크립트의 기능

### 크로스 플랫폼 지원

자바스크립트가 실행되는 모든 플랫폼에서 사용할 수 있다

### 객체 지향 언어

클래스, 인터페이스, 모듈 등의 강력한 기능을 제공하며, 순수한 객체 지향 코드를 작성할 수 있다

### 정적 타입

### DOM 제어

자바스크립트와 같이 DOM을 제어해 요소를 추가하거나 삭제할 수 있다

### 최신 ECMAScript 지원

ES6 이상의 최신 자바스크립트 문법을 손쉽게 지원한다

# 🙋타입스크립트 연습

## 생성

우선 디렉토리를 하나 생성한다

```
$ npm init -y
$ npm intall -g typescript
$ tsc --init // tsconfig.json 파일 자동생성 - 타입스크립트가 컴파일 될 때 필요한 옵션 지정
```

```javascript
// tsconfig.json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true
  }
}
```

| 옵션            | 의미                                                                                                                                                       |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| target          | 컴파일된 코드가 어떤 환경에서 실행될지 정의 </br> 예를들어서 화살표 함수를 사용하고 target을 es5로 하면 <br/>일반 function 키워드를 사용하는 함수로 변환함 |
| module          | 컴파일된 코드가 어떤 모듈 시스템을 사용할지 정의                                                                                                           |
| strict          | 모든 타입 체킹 옵션을 활성화                                                                                                                               |
| esModuleInterop | commonjs 모듈 형태로 이루어진 파일을 es2015 모듈 형태로 불러올 수 있게 해줌                                                                                |

## 선언

### 지정한 타입과 다른 지정 타입의 변수를 입력하면 에러남

![](https://images.velog.io/images/ouo_yoonk/post/719a74d6-bce3-4c90-8e12-2af1cb6df45b/image.png)

![](https://images.velog.io/images/ouo_yoonk/post/f9770bcb-dabf-437a-bc2f-2c872b7597f5/image.png)

## 실행

위의 스크립트를 다음 명령어로 실행하면 js 파일이 만들어짐

```
$ tsc
```

![](https://images.velog.io/images/ouo_yoonk/post/3e8347de-3f97-4f1e-9288-b72fcfcc005e/image.png)

![](https://images.velog.io/images/ouo_yoonk/post/3d15a84b-323e-48d0-b1a6-d4b486548cef/image.png)

## 기본 타입

- 숫자, 문자, boolean
- 타입 배열 (ex-number[])
- null, undefined
- | 연산자

```typescript
// 숫자(선언x)
let count = 0;
count += 1; // count = '갑자기 분위기 문자열' 하면 에러남

// 문자
const message: string = 'hello world';

// boolean
const done: boolean = true;

// 타입 배열
const numbers: number[] = [1, 2, 3];
const messages: string[] = ['hello', 'world'];

messages.push('gg'); //push(1) 에러남

// undefined, null
let mightBeUndefined: string | undefined = undefined;
let nullableNumber: number | null = null;

// | 연산자
let color: 'red' | 'orange' | 'yellow' = 'red';
color = 'yellow'; //color = 'green';
```

## 함수에서 타입 정의하기

- parameter 타입, return 값 타입(return이 없으면 void)

```typescript
function sum(x: number, y: number): number {
  // parameter 타입, 결과값 타입
  return x + y;
  // return null; number를 반환한다고 하고 null을 반환하면 에러
}

sum(1, 2);
```

## interface 사용해보기

interface는 클래스 또는 객체를 위한 타입을 지정 할 대 사용하는 문법

### implements

```typescript
interface Shape {
  getArea(): number;
  // shape interface에는 getArea라는 함수가 꼭 있어야하며,
  // 해당 함수의 반환값은 숫자
}

class Circls implements Shape {
  radius: number;
  constructor(radius: number) {
    this.radius = radius;
  }

  getArea() {
    return this.radius * this.radius * Math.PI;
  }
}
```

## Type Alias 사용하기

## Generics

---

**reference**

- https://heropy.blog/2020/01/27/typescript/
- https://react.vlpt.us/using-typescript/
