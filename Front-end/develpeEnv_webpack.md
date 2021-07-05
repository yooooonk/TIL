# 웹팩

> 웹팩(Webpack 또는 webpack)은 오픈 소스 자바스크립트(JS) 모듈 번들러이다. 웹팩은 의존성이 있는 모듈을 취하여 해당 모듈을 대표하는 정적 자산들을 생성한다.

- 여러 개의 모듈을 하나의 파일로
- 주로 자바스크립트(JS)를 위한 모듈 번들러이지만 호환 플러그인을 포함하는 경우 HTML, CSS, 심지어는 이미지와 같은 프론트엔드 자산들을 변환할 수 있다.
- 웹팩은 의존성을 취한 다음 의존성 그래프를 만듦으로써 웹 개발자들이 웹 애플리케이션 개발 목적을 위해 모듈 방식의 접근을 사용할 수 있게 도와준다.
- 명령 줄을 통해서 사용할 수 있으며, "webpack.config.js"이라는 이름의 구성 파일을 사용하여 구성할 수 있다. 이 파일을 사용하면 프로젝트를 위해 로더, 플러그인 등을 정의할 수 있다. (웹팩은 로더를 통해 상당한 확장이 가능하므로 개발자들이 파일을 함께 번들링할 때 수행하기 원하는 사용자 지정 작업을 작성할 수 있다.)

# 웹팩이 필요한 이유

## 모듈 시스템

- 문법 수준에서 모듈을 지원하기 시작한 것은 ES2015부터 - import/export 구문

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

위의 방식으로 파일을 불러올 경우 전역스코프가 오염됨

### IIFE 방식의 모듈

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

- 자바스크립트를 사용하는 모든 환경에서 모듈을 하는 것이 목표

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

# 엔트리와 아웃풋

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

### 명령어로 실행

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

---

**&#128209; reference**

- [위키백과 - 웹팩](https://ko.wikipedia.org/wiki/%EC%9B%B9%ED%8C%A9)
- [김정환 - 프론트엔드 개발환경의 이해:NPM](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)
