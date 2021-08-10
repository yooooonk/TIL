![](https://images.velog.io/images/ouo_yoonk/post/918f983e-2fcf-453e-8298-fdf23e130a88/DOM__n(Document__nObject_n_Model).png)



# DOM(Document Object Model)
> HTML이나 XML 문서의 프로그래밍 interface이다. 
- 문서의 구조화된 표현 제공
- 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공해 문서를 표현하고, 저장하고, 조작하는 방법을 제공한다.

 
HTML이나 XML Document 구조를 바탕으로 요소들이 화면에 나타나고, 이벤트에 반응하고 값을 입력받는 등의 기능을 수행할 객체들로 실체화 된 형태를 의미한다. 구조화된 nodes와 property와 method를 갖고 있는 objets로 문서를 표현한다. 이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 담당한다. DOM은 javascript를 이용해 명령을 받을 수 있지만 javascript 객체는 아니며, 언어에 종속되지 않고 DOM을 조작할 수 있다. (javascript, 파이썬 beautifulsoup 등) DOM은 웹 페이지의 객체 지향 표현이며, 자바스크립트와 같은 스크립팅 언어를 이용해 DOM을 수정할 수 있다.


## Node

![](https://media.vlpt.us/images/mollog/post/562dc77f-a541-4cb4-8858-47291c620b87/image.png)
https://velog.io/@mollog/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC%EC%99%80-%EC%A4%91%EC%9A%94%ED%95%9C-%EC%9B%90%EC%B9%99

  
- DOM의 요소들은 node를 상속받기 때문에 textContent, childNodes, firstChild, lastChild, parentNode, cloeNode, appendChild 등 node의 기능을 전부 갖고 있다. 그리고 node는 `eventTarget` 을 상속받기 때문에 addEventListener등의 기능을 갖고 있다.
- _Event Target method_ : `addEventListner`, `removeEventListner`, `dispatchEvent`
- html element는 노드고, 노드는 event target이기 때문에 이벤트 관련된 메소드를 사용할 수 있다.
- 각 요소마다 고유의 기능도 있다. ex) a - href,target, img - src
- CSS는 CSS Object Model을 가짐. 트리형식. 브라우저는 DOM+CSSOM을 이용해 화면을 그림
- BOM : Browser Object Model - 브라우저 자체를 다루는 api. ex)alert, setTimeout, ..

## DOM tree

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DOM-model.svg/1200px-DOM-model.svg.png)
https://ko.wikipedia.org/wiki/%EB%AC%B8%EC%84%9C_%EA%B0%9D%EC%B2%B4_%EB%AA%A8%EB%8D%B8

> `node`들의 `트리 구조`로 이루어져있다.


# Virtual DOM
>Virtual DOM (VDOM)은 UI의 이상적인 또는 “가상”적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 “실제” DOM과 동기화하는 프로그래밍 개념

- Virtual DOM은 SPA에서 사용하면 DOM의 구조만 간결히 흉내낸 자바스크립트 객체
- 실제 DOM을 조작하는 것은 무겁기 때문에 가벼운 가상DOM을 만들어, 실ㅈ ㅔDOM과 비교해 바뀐 부분만 실제 DOM을 조작해 반영.
- 런타임에서 작동함. 브라우저가 js 파일(라이브러리)을 받아서 DOM을 그리고 최소한의 변경으로 구현하는 방법을 찾는 방식

## Svelte
- 가상 DOM 없이 조작을 하기 때문에 리액트, 뷰보다는 빠름
- Svelte은 컴파일러이기 때문에 런타임 환경이 아닌 배포되기 전에 위의 과정이 일어남


---
__&#128209; reference__
- [MDN DOM](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)
- [React - Virtual DOM과 Internals](https://ko.reactjs.org/docs/faq-internals.html)
- [얄팍한 코딩 - DOM은 뭐고 가상 DOM은 뭔가요?](https://www.youtube.com/watch?v=1ojA5mLWts8&t=22s)