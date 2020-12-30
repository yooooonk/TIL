# Supertest
- nodejs http 서버를 테스트하기 위해 만들어진 모듈
- 통합테스트를 쉽게 구현할 수 있다

```javascript
const request = require('supertest');
const express = require('express');

const app = expresS()

// 클라이언트에서 들어오는 요청을 처리하는 원본소스
app.get('/user',function(res,res){
    res.status(200).json({name:'john'})
})

// 위에 원본 소스를 위한 통합테스트 소스
request(app)
    .get('/user')
    .expect('Context-type',/json/)
    .expect('Content-Length',15)
    .expect(200)
    .end(function(err,res){
        if(err) throw err;
    })
```