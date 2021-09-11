# 자바스크립트 런타임 환경

![](https://images.velog.io/images/ouo_yoonk/post/80801b55-c5cf-43f0-86d4-7bf39b3c8ff2/image.png)
출처 https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf

자바스크립트가 구동되는 환경을 이해하기 위해 공부하며 정리한 포스트입니다. 

자바스크립트는 기본적으로 싱글 쓰레드 기반 언어이기 때문에 호출 스택이 하나입니다. 따라서 한 번에 한 작업만 처리할 수 있습니다. 만약 호출 스택에 처리 시간이 오래 걸리는 함수가 있으면 그 작업을 처리하는 동안 브라우저는 멈추게 됩니다. 하지만 자바스크립트는 런타임 환경인 브라우저가 제공하는 멀티쓰레딩을 이용해 다양한 작업을 동시에 할 수 있습니다. 자바스크립트는 V8 엔진(Memory Heap + Call stack) + 브라우저가 제공하는 Web API + 이벤트루프 + 콜백 큐로 구성된 환경에서 동작합니다. 

## 자바스크립트 엔진 (V8)

크롬브라우저가 javascript 코드나 스크립트를 받으면 V8 엔진이 코드를 파싱합니다. 먼저 문법 오류를 먼저 검사합니다. 위에서부터 아래로 코드를 읽으며 JS 코드를 컴퓨터가 이해할 수 있는 기계어로 번역합니다. 

V8 엔진은 메모리힙과 콜스택을 가지고 있습니다.

### Memory Heap(메모리 힙)
변수나 함수 선언은 메모리 힙에 올라갑니다. 

### Call stack(호출 스택)
호출 스택에는 실행되는 코드가 쌓입니다. 스택에 함수가 추가되면 엔진은 그 코드를 파싱하고, 변수들을 힙에 올립니다. 현재 실행되고 있는 함수가 호출 스택의 가장 상단에 위치하는데, 함수가 값을 return하거나 web api를 호출하면 스택에서 제거(pop)되고, 그 다음 함수를 실행합니다. 호출 스택이 완전히 빌 때까지 이 과정을 반복합니다. 스택이 하나이기 때문에(싱글 스레드) 이 동기적이고, 한 번에 한 동작만 수행합니다.

## Web APIs
Web API는 event listner, HTTP/AJAX request, timing function(setTimeout) 등의 기능을 제공합니다. call stack에서 함수가 Web API를 실행하면 스택에서 제거되며, Web API의 콜백 함수는 큐에 저장됩니다.

## Callback Queue
콜백큐에는 콜백함수가 저장됩니다. Queue이기 때문에 먼저 들어온 것이 먼저 실행됩니다.(FIFO) 콜백큐에도 두 가지가 있습니다.


### Microtask Queue
Promise나 Mutation Observer의 콜백이 들어옵니다. Task Queue보다 우선순위가 높고, Event Loop는 빌 때까지 call stack에 콜백함수를 넣습니다.

### Task Queue
일반적인 콜백함수가 들어옵니다. Microtask Queue보다 우선 순위가 낮고, 가장 앞에 있는 콜백 함수만 Call Stack에 들어갑니다.

|Microtask Queue|Task Queue|
|--|--|
|Promise, Mutation Observer의 콜백 함수|이외의 콜백함수|
|우선 순위 높음|우선 순위 낮음|
|큐가 빌 때까지 event loop가 실행|제일 앞의 task만 실행|

### Render Seqeunce
변형한 코드를 화면에 업데이트하 위해 주기적으로 호출합니다. Request Animation Frame의 콜백이 전부 실행되면 Render Tree를 그리고 Layout, Paint 과정이 일어납니다.
예를 들어 아래와 같은 코드를 실행했을 때, 배경 색상이 노란색 되는 이유는 각각의 콜백을 모두 실행한 결과를 화면에 그리기 때문입니다. 

``` javascript
body.style.backgroundColor = 'red'
body.style.backgroundColor = 'blue'
body.style.backgroundColor = 'yellow'
```

## Event Loop
이벤트루프는 Call Stack이 비면 Task Queue의 콜백함수를 Call stack에 넣는 역할을 합니다. 이벤트루프가 아래의 그림처럼 순회합니다. Call stack의 function이 실행하는데 오래걸릴 때 화면에서 아무 변화가 없는 이유는 event loop가 Call stack에 머물러있어 다음 과정인 Render Sequene를 실행하지 못하기 때문입니다.


![](https://images.velog.io/images/ouo_yoonk/post/f77438e8-be79-4102-9ee9-b5936fcb1199/image.png)
출처 [드림코딩 - 프론트엔드 필수 브라우저101](https://academy.dream-coding.com/courses/browser101)



---
__📑 referece__
- [How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)
- [The Javascript Runtime Environment](https://olinations.medium.com/the-javascript-runtime-environment-d58fa2e60dd0)
- [MDN - 동시성 모델과 이벤트 루프](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)