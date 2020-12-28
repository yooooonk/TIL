# Node.js
---

- Node.js는 자바스크립트를 브라우저 외의 다른 환경에서도 사용할 수 있게 해주는 런타임
- http 서버가 내장되어 있기 때문에 보통은 서버로 많이 사용함

## npm
- node package manager
- Node.js에서는 자주 쓰이고 재사용되는 자바스크립트 코드들을 패키지도 만들어서 사용할 수 있다
- 이러한 패키지를 모아놓은 장소가 npm


### 기본 구조 코드 작성
- Package.json : 프로젝트의 정보와 프로젝트에서 사용 중인 패키지의 의존성을 관리하는 곳

```nodejs
npm init
```

- 사용할 모듈 추가
  - Express : Node.js의 API를 단순화하고 유용한 기능들은 더 추가해 Node.js를 더 편리하고 유용하게 사용할 수 있게 해주는 모듈
  - Mongoose : MongoDB를 편리하게 사용하게 해주는 노드의 확장 모듈
  ```
  npm i express mongoose --save
  ```
  - Jest : 단위테스트
  - node-mocks-http : 단위테스트
  - supertest : 통합 테스트
  ```
  npm install jest supertest node-mocks-http --save-dev
  ```
server.js
```javascript
// exporess module 불러오기
const express = require('express')

const PORT = 5000;

//applicaiton 생성
const app = express();
app.use(express.json()) //req.body를 사용하기위해

app.get('/',(req,res)=>{
    res.send('Hello World')
});

// applicaiton 시작
app.listen(PORT);
console.log(`Running on port ${PORT}`)

```

---

**reference**

- [인프런 - 따라하며 배우는 TDD 개발](https://www.inflearn.com/course/%EB%94%B0%EB%9D%BC%ED%95%98%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-tdd/dashboard)
- [Zero Cho](https://www.zerocho.com/category/NodeJS/post/57387cb8715202c8679b3af1)
