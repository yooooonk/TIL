# HttpXMLRequest 객체
- 서버와 상호작용하기 위해 사용됨
- 전체 페이지의 새로고침없이도 URL로부터 데이터를 받아올 수 있다
- AJAX 프로그래밍에 주로 사용
- XML뿐 아니라 모든 종류의 데이터를 받아오는 데 사용할 수 있다
- HTTP 이외의 프로토콜도 지원한다(file, ftp)
- 주요 속성 : reponse, status, statusText, responseText,...
- 주요 메서드 : open(요청 초기화), setRequestHeader(http 요청 헤더값을 설정), send(요청을 보냄)
``` javascript
const req = new XMLHttpRequest()
                req.open('GET','http://localhost:3000/health')
                req.send()
                req.addEventListener('load',()=>{
                    this.loading = false
                    this.apiRes = {
                        status : req.status,
                        statusText:req.statusText,
                        response:JSON.parse(req.response)
                    }
            })
```

# AJAX(Asynchronous JavaScrpt And XML)
- 자바스크립트의 라이브러리중 하나
- HTML, CSS, Javascript, DOM조작과 HMLHttpRequest Object를 활용한 프로그래밍 방식 -- 그 자체가 특정한 기술은 아님
- 전체 페이지가 다시 로드되지 않고 일부분만 업데이트하는 좀 더 복잡한 웹페이지를 만들 수 있게 해준다
- 비동기식으로 작업할 수 있다
- 페이지 전체를 다시 로드하는 방식이 아닌 요청한 데이터를 받아 일부분만 갱신하므로 자원과 시간을 아낄 수 있다
### 장점
- 웹페이지 속도 향상
- 비동기처리로 서버처리가 완료될때까지 기다리지 않아도된다
- 서버에서 data만 전송하면 되므로 전체적인 코딩양이 줄어든다
### 단점
- 히스토리 관리가 안된다
- 보안에 더 신경써야한다
- 연속적으로 데이터를 요청하면 서버 부하가 증가한다
- 통신중에 사용자에게 진행정보가 주어지지 않는다

# Axios
- XMLHttpRequest 요청을 생성한다
- nodejs에서도 http request를 만들 수 있다
- __promise 객체__ 를 이용하므로 간결하게 코딩할 수 있다
- request와 response 사이에 intercept 처리를 추가할 수 있다 ex) 인증
- 자동으로 JSON 데이터 변환
> npm install axios
```javascript
axios.get('http://localhost:3000/headlth')
            .then(res=>{
                this.apiRes = res.data
            })
            .catch(res=>{
                this.error = res.response.data
            })
            .finally(()=>{
                this.loading = false
            })

```
---
__reference__
- [MDN - XMLHttpRequest](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest)
- [MDN - AJAX](https://developer.mozilla.org/ko/docs/Glossary/AJAX)
- [코딩팩토리 - ajax](https://coding-factory.tistory.com/143)
- [axios](https://github.com/axios/axios)
