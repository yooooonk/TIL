![](https://images.velog.io/images/ouo_yoonk/post/3f687752-f918-4298-87a7-9d031b582309/Next_js.png)

# Next.js

> Next.js gives you the best developer experience with all the features you need for production: hybrid static & server rendering, TypeScript support, smart bundling, route pre-fetching, and more. No config needed.

## 특징

- Imgage component(next/image) 최적화 : resizing, servering image를 제공
- config 설정이 필요없이 자동으로 번들링됨
- SSR 제공
- 코드 스플리팅 자동화로 빠른 페이지 로드 가능
- Babel, Webpack 설정 커스터마이징 가능
- 디렉토리 구조로 라우팅 기능

## 기본 구조

```javascript
pages / // HTML Document, Application Container, 각종 페이지 등을 작성한다.
  _document.js; // SPA 시작점이 되는 index.html
_app.js; // Application Container. 공통의 레이아웃을 작성한다.
_error.js; // Error Page.
index.js; // Root Page /로 시작되는 경로를 말한다.
hello.js; // Hello Page /hello로 시작되는 경로를 말한다.
static / // 정적 파일 (이미지, 파일 등)을 업로드 한다.
  next.config.js; // Next.js의 환경 설정 파일이다. 라우팅 설정, typescript, less 등의 webpack 플러그인을 설정한다.
```

## SSR

[ssr 정리 글](https://velog.io/@ouo_yoonk/Next.js)

> 1. Frontend server에서 GET 요청을 받는다
> 2. 요청에 맞는 page를 찾는다
> 3. \_app.js의 getinitialProps가 있다면 실행
> 4. Page Component 안에 getinitailProps가 있다면 실행
> 5. \_document.js의 getInitalProps가 있다면 실행
> 6. 모든 props를 구성하고 \_app.js > Page Component 순으로 렌더링
> 7. 모든 콘텐츠를 구성하고 \_document.js를 실행해 html 형태로 출력

### getInitailProps

웹 페이지는 각 페이지마다 사전에 불러와야할 데이터들이 있다. Data Fectching이라고도 하는 로직은 CSR(Client Side Rendering)에서는 react 로직에 따라 componentDidMount or useEffect로 컴포넌트가 마운트 되고 나서 하는 경우가 많다. 이 과정을 서버에서 미리 처리하도록 도와주는 것이 바로 getInitialProps이다. (사실 Data Fetching에만 getInitialProps를 사용할 수 있는 것은 아니다.)

```javascript
import axios from 'axios';

const Page = ({ stars }) => {
  return <div>Next stars: {stars}</div>;
};

Page.getInitialProps = async (ctx) => {
  const { data } = await axios.get('...url');

  return { stars: data };
};

export default Page;
```

- getInitialProps 내부 로직은 서버에서 실행된다. 따라서 client에서만 가능한 로직(dispatch, 자바스크립트 내장객체 등)은 사용 불가능하다
- 한 페이지를 로드할 때 하나의 getInitialProps 로직만 실행된다.

---

**&#128209; reference**

- https://nextjs.org/
- https://medium.com/@msj9121/next-js-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%95%8C%EA%B3%A0-%EC%93%B0%EC%9E%90-8727f76614c9
- https://velog.io/@cyranocoding/Next-js-%EA%B5%AC%EB%8F%99%EB%B0%A9%EC%8B%9D-%EA%B3%BC-getInitialProps
- https://salgum1114.github.io/nextjs/2019-05-06-nextjs-static-website-1/
