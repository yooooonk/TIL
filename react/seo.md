# SEO (Search Engin Optimiztion)

검색 엔진 최적화. 네이버나 구글같은 검색 엔진에 뭔가를 검색했을 때, 내가 만든 사이트가 검색 결과에 더 잘 보이게 하기 위한 과정.

검색을 하면,
검색 엔진이 내 사이트 내용물(meta tag나 html 등)을 훑어가고 내용물에 특정한 인덱스 같은 것을 만들어 검색 결과에 보여준다.

검색 엔진 최적화는 검색엔진이 내 사이트를 크롤링할 때 정보를 더 잘 가져갈 수 있도록 도와주는 과정이기도 하다.

## react에서 SEO?

React는 HTML 파일이 딱 1개 뿐이고, 렌더링이 되기 전까지(javascript를 실행하기 전까지)는 껍데기 html만 있어, 기본적으로는 검색 엔진에 올라가기 어렵다. 그래서 react에서도 검색 엔진이 긁어갈 수 있도록 미리 html 파일 내용을 보여줄 필요가 있다.

1. meta-tag
2. pre-rendring
3. server side rendering

# pre-rendering

> 빌드할 때 미리 특정 페이지를 렌더링해서 html 파일을 만들어 두는 것

SPA는 사용자가 실제 콘텐츠를 보기전에 사이트를 구성하는 javascript 번들이 다운로드를 완료할 때까지 기다려야하고, 번들이 클수록 더 오래 기다려야한다.

SSR은 브라우저에서 부팅하는 대신 서버에서 응용 프로그램을 렌더링하는 방식이다. 각 페이지/경로 전환과 함게 완전한 HTML이 서버에서 생성되고 브라우저로 전송되므로 첫 번째 페인트 시간(FCP)이 줄어들지만, 첫 번째 바이트까지 걸리는 시간(TTFB)은 느려질 수 있다.

pre-rendering은 ssr보다 덜 복잡하지만 응용 프로그램에서 첫 번째 페인트 시간을 개선하는 방법을 제공하는 별도의 기술이다.

빌드할 때 html 파일을 만들어두기 때문에 검색 엔진이 크롤링하러 사이트에 들어왔을 때, 빈 껍데기 html 파일 대신 내용물을 가져갈 수 있다.

하지만, pre-rendering 첫 번째 요청에서 그대로 전송되는 정적인 파일만을 가져오는 것이므로, _서버측 데이터는 없다._

## react-snap

1. 패키지 설치
   `yarn add --dev react-snap`

2. package.jso에 script 추가
   `postbuild:'react-snap'`

3. index.js 수정

```javascript
import { hydrate, render } from 'react-dom';

const rootElement = document.getElementById('root');
if (rootElement.hasChildNodes()) {
  hydrate(<App />, rootElement);
} else {
  render(<App />, rootElement);
}
```

4. package.json에 프리 렌더링 할 페이지 추가

```javascript
"reactSnap":{
    "include":["/two","/"]
  },
```

5. 빌드
   `yarn build`
   ![](https://images.velog.io/images/ouo_yoonk/post/7464c017-c349-42f0-9735-81882bb44b42/image.png)

6. 실행해서 확인하기

```javascript
// server.json 추가
{
    "rewrites": [
      { "source": "/", "destination": "/200.html" },
      { "source": "/two", "destination": "/two/index.html" }
    ]
  }
```

```
$ yarn global add serve

serve - c serve.json build
```

![](https://images.velog.io/images/ouo_yoonk/post/b4b23e91-9ae0-4db9-8d27-72cbbddaf156/image.png)
localhost:5000에서 build가 잘 되었는지 확인할 수 있음!

## Server-side rendering

- [SSR](https://velog.io/@ouo_yoonk/Next.js)

> SSR은 서버에서 사용자에게 보여줄 페이지에 필요한 데이터를 가지고 와 미리 채운 다음에 페이지를 로드하는 방식

서버에서 페이지를 구성하기 때문에 클라이언트에서 구성하는 CSR보다 페이지를 구성하는 속도는 늦어지지만 전체적으로 사용자에게 보여주는 콘텐츠 구성이 완료되는 시점이 빨라진다.

## Next.js로 SSR하기

![](https://images.velog.io/images/ouo_yoonk/post/97a5274b-a276-4420-b0a9-29a3d5877e5c/image.png)

```javascript
// configureStore - next js + redux 사용을 위한 설정
import { createWrapper } from 'next-redux-wrapper';
import { applyMiddleware, compose, createStore } from 'redux';
import reducer from '../reducers';
import rootSaga from '../sagas';
import { composeWithDevTools } from 'redux-devtools-extension';
import createSagaMiddleware from 'redux-saga';

const configureStore = () => {
  const sagaMiddleware = createSagaMiddleware();
  const middlewares = [sagaMiddleware];

  const enhancer =
    process.env.NODE_ENV === 'production'
      ? compose(applyMiddleware(...middlewares))
      : composeWithDevTools(applyMiddleware(...middlewares));

  const store = createStore(reducer, enhancer);
  store.sagaTask = sagaMiddleware.run(rootSaga);
  return store;
};

const wrapper = createWrapper(configureStore, {
  debug: process.env.NODE_ENV === 'development'
});

export default wrapper;
```

```javascript
// _app.js
import wrapper from '../store/configureStore';

const App = ({ Component }) => {
  return (
    <>
      <Head>
        <title>NodeBird</title>
      </Head>
      <Component />
    </>
  );
};

App.Proptypes = {
  Component: Proptypes.elementType.isRequired
};

export default wrapper.withRedux(App); // nextjs-redux
```

### getServerSideProps

- 빌드와 상관없이, 매 요청마다 데이터를 서버로부터 가져옴

```javascript
// index.js
import wrapper from "../store/configureStore";
import {END} from 'redux-saga';

const Home () => {
	...
}

export const getServerSideProps = wrapper.getServerSideProps((context)=>{
  //로그인 쿠키공유
  const cookie = context.req? context.req.headers.cookie : '';
    axios.defaults.headers.Cookie = '';
    if(context.req && cookie){
        axios.defaults.headers.Cookie = cookie;
    }

    axios.defaults.headers.Cookie = cookie;
  // 데이터 요청
    context.store.dispatch({
        type:LOAD_USER_REQUEST
    });

    context.store.dispatch({
        type:LOAD_POST_REQUEST
    });

    context.store.dispatch(END);
    await context.store.sagaTask.toPromise()
})

export default Home;

```

### getStaticProps

- 빌드시 고정되는 값으로, 빌드이후에는 변경이 불가능하다

```javascript
export const getStaticProps = wrapper.getStaticProps(async (context) => {
  console.log('getStaticProps');
  context.store.dispatch({
    type: LOAD_USER_REQUEST,
    data: 1
  });
  context.store.dispatch(END);
  await context.store.sagaTask.toPromise();
});
```

## Client Side Rendering

![](https://images.velog.io/images/ouo_yoonk/post/5076c387-6c73-4337-8fdc-ed1d74037619/image.png)
![](https://images.velog.io/images/ouo_yoonk/post/408088a3-b9de-47eb-9f7c-058ff5698a39/image.png)

> 데이터없이 화면만 받고 데이터 로딩창을 띄우면서 백엔드에 데이터를 요청해 화면을 렌더링

- 페이지가 한번 로딩된 이후에는 데이터를 수정하거나 조회할 때, 페이지가 새로 고침되지 않고 다른 페이지로 넘어가지 않는다
- react, vue, agular등에서 사용하는 방식
- SPA인 경우에도 첫 방문은 SSR으로 가져오는 경우가 많다

---

**reference**

- https://web.dev/prerender-with-react-snap/
- 스파르타 코딩클럽 리액트 심화 강의
- [인프런 - react로 nodebird sns만들기](https://www.inflearn.com/course/%EB%85%B8%EB%93%9C%EB%B2%84%EB%93%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A6%AC%EB%89%B4%EC%96%BC#)
- [getStaticProps와 getServerSideProps in next.js](https://medium.com/%EB%8F%84%EA%B9%A8%EB%B9%84-%EC%9D%B4%EC%95%BC%EA%B8%B0/getstaticprops%EC%99%80-getserversideprops-in-next-js-ab076c253d2c)
- https://d2.naver.com/helloworld/7804182
- [아몽소프트웨어](https://medium.com/%EC%95%84%EB%AA%BD%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4/csr-ssr-spa-mpa-ede7b55c5f6f)
