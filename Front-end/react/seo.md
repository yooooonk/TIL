# SEO (Search Engin Optimiztion)

- 검색 엔진 최적화
- 네이버나 구글같은 검색 엔진에 뭔가를 검색했을 때, 내가 만든 사이트가 검색 결과에 더 잘 보이게 하리 위한 과정

검색을 하면,
검색 엔진이 내 사이트 내용물(meta tag나 html 등)을 훑어가고 내용물에 특정한 인덱스 같은 것을 만들어 검색 결과에 보여줌

검색 엔진 최적화는 검색엔진이 내 사이트를 크롤링할 때 정보를 더 잘 가져갈 수 있도록 도와주는 과정이기도 함

## react에서 SEO?

- React는 HTML 파일이 딱 1개 뿐이고, 렌더링이 되기 전까지(javascript를 실행하기 전까지)는 껍데기 html만 있어, 기본적으로는 검색 엔진에 올라가기 어렵다. 그래서 react에서도 검색 엔진이 긁어갈 수 있도록 미리 html 파일 내용을 보여줄 필요가 있다.

1. meta-tag 넣기
2. pre-rendring
3. server side rendering

# pre-rendering

- 빌드할 때 미리 특정 페이지를 렌더링해서 html 파일을 만들어 두는 것. 검색 엔진이 크롤링하러 사이트에 들어왔을 때, 빈 껍데기 html 파일 대신 내용물을 가져갈 수 있음검색 엔진이 크롤링하러 사이트에 들어왔을 때, 빈 껍데기 html 파일 대신 내용물을 가져갈 수 있음
- react-snap 이용

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

6. 실행

```javascript
{
    "rewrites": [
      { "source": "/", "destination": "/200.html" },
      { "source": "/two", "destination": "/two/index.html" }
    ]
  }
```
