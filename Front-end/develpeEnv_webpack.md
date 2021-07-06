# 1. 웹팩

> 웹팩(Webpack 또는 webpack)은 오픈 소스 자바스크립트(JS) 모듈 번들러이다. 웹팩은 의존성이 있는 모듈을 취하여 해당 모듈을 대표하는 정적 자산들을 생성한다.

- 여러 개의 모듈을 하나(혹은 여러개의)의 파일로 변환
- 주로 자바스크립트(JS)를 위한 모듈 번들러이지만 호환 플러그인을 포함하는 경우 HTML, CSS, 심지어는 이미지와 같은 프론트엔드 자산들을 변환할 수 있다.
- 웹팩은 의존성을 취한 다음 의존성 그래프를 만듦으로써 웹 개발자들이 웹 애플리케이션 개발 목적을 위해 모듈 방식의 접근을 사용할 수 있게 도와준다.
- 명령 줄을 통해서 사용할 수 있으며, "webpack.config.js"이라는 이름의 구성 파일을 사용하여 구성할 수 있다. 이 파일을 사용하면 프로젝트를 위해 로더, 플러그인 등을 정의할 수 있다. (웹팩은 로더를 통해 상당한 확장이 가능하므로 개발자들이 파일을 함께 번들링할 때 수행하기 원하는 사용자 지정 작업을 작성할 수 있다.)

## 역할

- 리소스를 묶어주는 역할
- 변화를 감지해 업무를 다시 실행
- 바벨을 활용해 ES5로 코드 변환, 브라우저와 상관없이 최신 자바스크립트 기능을 사용할 수 있게 해줌
- 커피스크립트를 자바스크립트로 컴파일
- 인라인 이미지를 데이터 URIs로 변환
- CSS 파일을 import 할 수 있음
- 개발 웹서버를 실행시킬 수 있음
- 핫 모듈을 대신해서 사용할 수 있음
- 첫 화면이 로드될 때 큰 자바스크립트 파일이 불려지는 것을 피하기위해 출력 파일을 여러개로 나눌 수 있음
- tree shaking을 만들 수 있음

## 모듈 시스템

- import/export 구분으로 문법 수준에서 모듈을 지원하기 시작한 것은 ES2015부터
- 모듈 시스템이 아닌 방식으로 파일을 불러올 경우 전역스코프가 오염됨

**예시코드**

```javascript
// math.js
function sum(a, b) {
  return a + b;
}
```

```javascript
// app.js
console.log(sum(1, 2));
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script src="src/math.js"></script>
    <script src="src/app.js"></script>
  </body>
</html>
```

### IIFE(즉시 실행함수) 방식의 모듈

- 첫번재 괄호 안에 익명함수를 정의하는 방식
- 함수와 변수를 전역 스코프가 아닌 함수 스코프로 제한할 수 있다.

```javascript
var math = math || {};

(function () {
  function sum(a, b) {
    return a + b;
  }

  math.sum = sum;
})();
// math.sum(a,b)으로 접근가능
```

### CommonJS

CommonJS(http://www.commonjs.org/) 는 JavaScript를 브라우저에서뿐만 아니라, 서버사이드 애플리케이션이나 데스크톱 애플리케이션에서도 사용하려고 조직한 자발적 워킹 그룹이다. 이 그룹은 JavaScript를 범용적으로 사용하기 위해 필요한 '명세(Specification)'를 만드는 일을 한다.

자바스크립트가 브라우저용 언어를 범어 범용적으로 쓰이려면 `모듈화`가 필요했고, CommonJS의 주요 명세는 이 모듈을 어떻게 정의하고, 어떻게 사용할 것인가에 대한 것이다.

- Scope : 모든 모듈은 자신만의 독립적인 실행 영역이 있어야 한다.
- Definition : 모듈 정의는 exports 객체를 이용한다
- Usage : 모듈 사용은 require 함수를 이용한다.

```javascript
// math.js
exports function sum(a,b){
    return a+b;
}
```

```javascript
// app.js
const sum = require('./math.js');
console.log(sum(1, 2));
```

### AMD

또 다른 Javascript 표준 API 라이브러리 제작 그룹이다. 비동기 상황에서도 Javascript 모듈을 쓰기 위해 CommonJS에서 함께 논의하다 합의점을 이루지 못하고 독립했다. AMD의 목표는 필요한 모듈을 네트워크를 이용해 내려받아야 하는 브라우저 환경에서도 모듈을 사용할 수 있도록 표준을 만드는 일이다. CommonJS와 같이 require() 함수를 사용할 수 있고, exprts 형태로 모듈을 정의한다. AMD만의 특징인 define() 함수는 파일 스코프의 역할을 한다. 브라우저 환경의 javascript는 파일 스코프가 따로 존재하지 않기 때문에, 이 함수가 일종의 네임스페이스 역할을 해 모듈에서 사용하는 변수와 전역변수를 분리한다.

### 표준 모듈 시스템

```javascript
// math.js
export function sum(a, b) {
  return a + b;
}
```

```javascript
// app.js
import * as math from './math.js';

console.log(math.sum(1, 2));
```

그러나 모듈 시스템을 지원하지 않는 브라우저가 있다. 브라우저에 무관하게 모듈을 사용하고 싶을 때!! `웹팩`을 사용함!!!!

# 2.엔트리와 아웃풋

![](https://images.velog.io/images/ouo_yoonk/post/d61e0cb0-4667-463a-aa81-87a9105aacd6/image.png)

웹팩설치

```
$ npm install -D webpack webpack-cli
```

![](https://images.velog.io/images/ouo_yoonk/post/804d78c1-3485-44d7-b96e-19eeafe5f782/image.png)

## 웹팩 번들링 실습

### 필수옵션

- mode : development, production(배포용 옵션), none
- entry : 모듈의 시작점
- output : entry를 통해 모듈을 하나로 합치고, 결과를 저장하는 경로를 설정하는 옵션

### 명령어로 실행해보기

아래의 명령어로 번들링하면 gist/main.js에 번들링 된 파일이 생김
![](https://images.velog.io/images/ouo_yoonk/post/18e7924b-238c-4b2c-aacc-d836220e6332/image.png)
![](https://images.velog.io/images/ouo_yoonk/post/b9b5358b-3c0e-4055-b6b7-e6f1ac36f298/image.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script src="dist/main.js"></script>
  </body>
</html>
```

### 웹팩 설정파일 - webpack.config.js

```javascript
const path = require('path');

module.exports = {
  mode: 'development',
  entry: {
    main: './src/app.js' // 아웃풋 이름을 동적으로 생성할 수 있음
  },
  output: {
    path: path.resolve('./dist'),
    filename: '[name].js'
  }
};
```

- package.json파일에 build를 webpack으로 설정하면 웹팩 설정파일을 읽어와 번들링함 -- `npm run build`
  ![](https://images.velog.io/images/ouo_yoonk/post/03172b6c-fd2b-4163-92bd-80a12a889d3d/image.png)

# 3.로더

웹팩은 모든 파일을 모듈로 바라본다. 자바스크립트로 만든 모듈 뿐만 아니라 스타일시트, 이미지, 폰트까지도 전부 모듈로 보기 때문에 imort 구문을 사용하면 자바스크립트 코드 안으로 가져올 수 있다.

이것이 가능한 이유는 웹팩의 `로더` 덕분이다. 로더는 타입스크립트 같은 다른 언어를 자바스크립트 문법으로 변환해 주거나 이미지를 data URL 형식의 문자열로 변환한다. 뿐만 아니라 CSS 파일을 자바스크립트에서 직접 로딩할 수 있도록 해준다.

## 로더의 동작원리 이해 - 커스텀로더 만들기

- 로더는 함수형태
- 로더가 읽은 파일이 parameter로 들어와 필요한 조작을 해서 반환

**my-webpack-loader.js**

```javascript
// my-webpack-loader.js
module.exports = function myebpackLoader(content) {
  console.log('myWebpackLoader가 동작함');
  return content;
};
```

**webpack.config.js**

![](https://images.velog.io/images/ouo_yoonk/post/4e99d68b-386c-4502-ac26-211de147b791/image.png)

- 로더는`module 객체에 rules`의 배열에 들어감
- `test`는 로더가 처리해야할 파일의 패턴 - 정규표현식을 사용한다. 위 예제의 경우 모든 자바스크립트 파일마다 로더가 실행됨
- `use`는 패턴에 걸리면 실행될 로더 함수들을 명시. 배열 뒤에 순서부터 실행됨

## 자주 사용되는 로더

### css-loader, style-loader

- javascript에서 css 파일을 모듈로 불러올 수 있음
- css-loader : css파일을 js 모듈로
- style-lodader : 변환된 css js 모듈을 html에 적용
  `$ npm install css-loader style-loader` 설치

![](https://images.velog.io/images/ouo_yoonk/post/9bc36967-369b-4185-8e3a-b40bded7bdfa/image.png)

### file-loader

`$ npm install file-loader` 설치
![](https://images.velog.io/images/ouo_yoonk/post/f3dbbe9f-ec56-4487-8e1c-01dd85185cf6/image.png)

### url-loader

사용하는 이미지 갯수가 많다면 네트웍 리소스를 사용하는 부담이 있고 사이트 성능에 영향을 줄 수도 있다. 만약 한 페이지에서 작은 이미지를 여러개 사용한다면 Data URI Scheme(작은 파일을 Base64로 인코딩하여 문자열 형태로 소스코드에 넣는 형식)를 이용하는 방법이 더 낫다. url-loader는 이런 처리를 자동화해준다.
`$ npm install -D url-loader`
![](https://images.velog.io/images/ouo_yoonk/post/7c0903ca-d507-4a8b-b263-238619146372/image.png)

---

**&#128209; reference**

- [위키백과 - 웹팩](https://ko.wikipedia.org/wiki/%EC%9B%B9%ED%8C%A9)
- [yngmanie블로그 - 초보자를 위한 웹팩 소개](https://yngmanie.space/posts/Abeginner%E2%80%99sIntroductionToWebpack)
- [naverD2 - 자바스크립트 표준을 위한 움직임 : CommonJS와 AMD](https://d2.naver.com/helloworld/12864)
- [김정환 - 프론트엔드 개발환경의 이해:NPM](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)
