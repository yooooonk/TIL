## Server Side Rendering

![](https://images.velog.io/images/ouo_yoonk/post/8eaa3b3f-5a1d-4022-b7dc-b14319869a59/image.png)

> SSR은 서버에서 사용자에게 보여줄 페이지를 모두 구성해 사용자에게 페이지를 보여주는 방식

- JSP/Servlet의 아키텍처에서 사용하는 방식
- 서버에서 페이지를 구성하기 때문에 클라이언트에서 구성하는 CSR보다 페이지를 구성하는 속도는 늦어지지만 전체적으로 사용자에게 보여주는 콘텐츠 구성이 완료되는 시점이 빨라진다.
- SEO(search engine optimization) 또한 쉽게 구성할 수 있다(CSR은 페이지에 로딩창만 있어 검색엔진이 상위에 노출시키지 않는 경우가 있음)

## Client Side Rendering

![](https://images.velog.io/images/ouo_yoonk/post/5076c387-6c73-4337-8fdc-ed1d74037619/image.png)
![](https://images.velog.io/images/ouo_yoonk/post/408088a3-b9de-47eb-9f7c-058ff5698a39/image.png)

> 데이터없이 화면만 받고 데이터 로딩창을 띄우면서 백엔드에 데이터를 요청해 화면을 렌더링

- 페이지가 한번 로딩된 이후에는 데이터를 수정하거나 조회할 때, 페이지가 새로 고침되지 않고 다른 페이지로 넘어가지 않는다
- react, vue, agular등에서 사용하는 방식
- SPA인 경우에도 첫 방문은 SSR으로 가져오는 경우가 많다

## Next.js로 SSR하기

![](https://images.velog.io/images/ouo_yoonk/post/97a5274b-a276-4420-b0a9-29a3d5877e5c/image.png)

```javascript
// configureStore
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

export default wrapper.withRedux(App);
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

---

**&#128209; reference**

- [인프런 - react로 nodebird sns만들기](https://www.inflearn.com/course/%EB%85%B8%EB%93%9C%EB%B2%84%EB%93%9C-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A6%AC%EB%89%B4%EC%96%BC#)
- [getStaticProps와 getServerSideProps in next.js](https://medium.com/%EB%8F%84%EA%B9%A8%EB%B9%84-%EC%9D%B4%EC%95%BC%EA%B8%B0/getstaticprops%EC%99%80-getserversideprops-in-next-js-ab076c253d2c)
- https://d2.naver.com/helloworld/7804182
- [아몽소프트웨어](https://medium.com/%EC%95%84%EB%AA%BD%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4/csr-ssr-spa-mpa-ede7b55c5f6f)
