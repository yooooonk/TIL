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
Web API는 event listner, HTTP/AJAX request, timing function(setTimeout) 등

## Callback Queue
## Event Loop




webAPI가 실행될 때 콜백함수는 task Queue에 들어감
call stack과 task Queue를 감시하는 것이 `Event Loop`

call stack이 비었을 때 Event loop가 task Queue의 콜백함수를 call stack에 넣음!!

![](https://images.velog.io/images/ouo_yoonk/post/2382dada-b69f-4e90-b824-777308505d13/image.png)

- Task Queue
- Microtask Queue
    - 프로미스에 등록된 콜백(then), mutation observer의 콜백이 들어옴
- Render Sequence
    - 우리가 변형한 코드를 업데이트 하기 위해 주기적으로 호출하는 순서
    - Request Animation Frame--의 콜백

- 60fps - 브라우저는 1초동안 60개 프레임을 보여주도록 노력
- 이벤트루프는 저 순서로 순회
    - call stack에 뭐가 있으면 멈추어ㅣㅆ음
    - Render 들릴 ㅅ수도 있고 아닐 수도 있음
    - Microtask Queue가 빌 때까지 콜스택에 쌓음
        - microtask queue에 잇는 동안 계속 작업이 들어오면 거기에 멈춰있음
    - task queue는 아이템 하나만 콜스택으로 보냄


---
__📑 referece__
- [How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)
- [The Javascript Runtime Environment](https://olinations.medium.com/the-javascript-runtime-environment-d58fa2e60dd0)