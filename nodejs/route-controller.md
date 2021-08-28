# Router - controller 구조
>요청 ->server.js(진입점)->route -> controller

# Route 구현 방법
1. express.router 클래스를 이용해 router를 모듈로 작성하기
2. router에서 미들웨어 함수를 load하기
3. route 정의
4. 기본앱에서 경로에 따라 라우터 모듈을 마운트하기

server.js
```javascript

const express = require('express')

const PORT = 5000;

const app = express();
app.use(express.json()) //req.body를 사용하기위해

// 기본앱의 한 경로에 라우터 모듈을 마운트하기
const productRoutes = require('./routes')
app.use('/api/products',productRoutes)

app.listen(PORT);
console.log(`Running on port ${PORT}`)
```

route.js
``` javascript
// express.router 클래스를 이용해 router를 모듈로 작성하기
const express = require('express')
const router = express.Router()
const productController = require('./controller/products')

//router에서 미들웨어 함수를 load하기
router.get('/',productController.hello);

module.exports = router;
// 3. 몇몇 Route를 정의하기
```

controller/products.js
``` javascript
exports.hello = (req,res)=>{
    res.send('안녕하세요')    
}
```
---
__reference__
- [인프런 - 따라하며 배우는 TDD 개발](https://www.inflearn.com/course/%EB%94%B0%EB%9D%BC%ED%95%98%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-tdd/dashboard)
- [MDN - Express Tutorial Part 4: Routes and controllers](https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/routes)