![](https://images.velog.io/images/ouo_yoonk/post/504c6298-c689-45d5-a8f3-ef4b56e10159/HTTP%F0%9F%93%9C.png)

# URI 설계

## resource와 행위를 분리할 것

- Uniform Resource Identifitail
- **URI는 리소스**를 식별하는 것이다
<details>
<summary>REST 인터페이스의 원칙에 대한 가이드</summary>
<div markdown="1"><br/>
  1.자원의 식별<br>
	요청 내에 기술된 개별 자원을 식별할 수 있어야 한다. 웹 기반의 REST 시스템에서의 URI의 사용을 예로 들 수 있다. 자원 그 자체는 클라이언트가 받는 문서와는 개념적으로 분리되어 있다. 예를 들어, 서버는 데이터베이스 내부의 자료를 직접 전송하는 대신, 데이터베이스 레코드를 HTML, XML이나 JSON 등의 형식으로 전송한다. <br/><br/>
  2. 메시지를 통한 리소스의 조작
클라이언트가 어떤 자원을 지칭하는 메시지와 특정 메타데이터만 가지고 있다면 이것으로 서버 상의 해당 자원을 변경·삭제할 수 있는 충분한 정보를 가지고 있는 것이다.  <br/><br/>
  3. 자기서술적 메시지 <br>
  각 메시지는 자신을 어떻게 처리해야 하는지에 대한 충분한 정보를 포함해야 한다. 예를 들어 MIME type과 같은 인터넷 미디어 타입을 전달한다면, 그 메시지에는 어떤 파서를 이용해야 하는지에 대한 정보도 포함해야 한다. 미디어 타입만 가지고도, 클라이언트는 어떻게 그 내용을 처리해야할 지 알 수 있어야 한다. 메시지를 이해하기 위해 그 내용까지 살펴봐야 한다면, 그 메시지는 자기서술적이 아니다. 예를 들어, 단순히 "application/xml"이라는 미디어 타입은, 실제 내용을 다운로드 받지 않으면 그 메시지만 가지고는 무엇을 해야할지에 대해 충분히 알려주지 못한다.<br><br>
  4. 애플리케이션의 상태에 대한 엔진으로서 하이퍼미디어
  만약에 클라이언트가 관련된 리소스에 접근하기를 원한다면, 리턴되는 지시자에서 구별될 수 있어야 한다. 충분한 콘텍스트 속에서의 URI를 제공해주는 하이퍼텍스트 링크의 예를 들 수 있겠다.
</div>
</details>

## URI 계층 구조를 활용

- 계층 구조상 상위를 컬렉션으로 보고 복수 단어 사용을 권장

### 예시

| 기능      | 예시               | 리소스 위주 설계 |
| --------- | ------------------ | ---------------- |
| 목록 조회 | /read-member-list  | /members         |
| 단일 조회 | /read-member-by-id | /members/{id}    |
| 등록      | /create-member     | /members/{id}    |
| 수정      | /update-member     | /members/{id}    |
| 삭제      | /delete-member     | /members/{id}    |

회원 resouce를 URI에 맵핑한다.
동사형으로 URI를 사용하지 않고, _HTTP 메서드를 통해 행위를 분리한다!_

## URI 설계 개념

### 문서(document)

단인 개념

### 컬렉션(collection)

- `서버`가 관리하는 리소스 directory
- 서버가 리소스의 URI를 생성하고 관리한다

### 스토어(store)

- `클라이언트`가 관리하는 자원 저장소
- 클라이언트가 리소스의 URI를 알고 관리한다

### 컨트롤 URI

- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스를 실행한다
- 동사를 직적 사용
  ex] /memebers/{id}/delete

# HTTP 메서드의 종류

## GET

`GET /members` `GET /members/100`

- 리소스 조회
- 서버에 전달하고 싶은 데이터를 query로 전달한다
- 메시지 바디도 사용 가능하지만 권장하지 않음

## POST

- 요청 데이터를 처리하는 모든 기능을 수행
- 메시지 바디를 통해 서버로 요청 데이터를 전달한다

### 기능

1. 새 리소스 생성
   서버가 아직 식별하지 않은 새 리로스 생성

2. 요청 데이터 처리
   단순히 데이터를 생성하거나 변경하는 것을 넘어 프로세스를 처리해야 하는 경우
   ex] 회원 등록, 주문에서 결제 완료->배달시작->배달완료처럼 단순히 값 변경을 넘어 프로세스 상태가 변경되는 경우
3. 다른 메서드로 처리하기 애매한 경우

## PUT

`PUT /members/100`

- 리소스가 있으면 대체, 없으면 생성한다.
- _완전히_ 덮어쓰기라고 생각하면 됨
- 클라이언트가 리소스를 식별하고, 클라이언트가 리소스 위치를 알고 URI를 지정한다

## PATCH

`PATCH /members/100`

- 기존 데이터를 부분적으로 변경한다
- PATCH를 지원안하는 서버도 있다

## DELETE

`DELETE /members/100`

- 데이터 삭제

## 기타

### HEAD

GET고 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환

### OPTIONS

- 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명
- 주로 CORS에서 사용

### CONNECT

대상 자원으로 식별되는 서버에 대한 터널을 설정

### TRACE

대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

## POST과 PUT의 차이

|                  | POST                                          | PUT                                                       |
| ---------------- | --------------------------------------------- | --------------------------------------------------------- |
| uri 예시         | POST /members                                 | PUT /files/{name}                                         |
| 리소스 관리 주체 | 서버<br>= 서버가 등록된 리소스 URI를 생성한다 | 클라이언트<br>= 클라이언트가 직접 리소스의 URI를 지정한다 |
|                  | collection                                    | store                                                     |

# 메서드의 속성

![](https://images.velog.io/images/ouo_yoonk/post/980ee19e-79d4-422b-b3c4-e4ae5edb8e18/image.png)

## 안전

- 호출해도 리소스를 변경하지 않는다.

## 멱등

- 호출 횟수에 상관없이 호출 결과가 똑같다.
- 자동 복구 메커니즘에 활용
- 서버가 정상 응답을 못했을 때, 클라이언트가 같은 요청을 다시 해도 되는가에 대한 판단근거가 된다
- GET, PUT, DELETE는 멱등
- POST는 멱등이 아니다. 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다

## 캐시

- 응답 결과 리소스를 캐시해서 사용해도 되는가?
- GET, HEAD, POST, PATCH는 캐시가 가능하나 실제로는 GET, HEAD 정도만 캐시로 사용한다.
- POST, PATCH는 구현이 쉽지 않다

# HTTP 메서드의 활용

## 클라이언트에서 서버로 데이터를 전송

- 쿼리 파라미터 : GET
- 메시지 바디 : POST,PUT,PATCH

### 정적 데이터 조회

- query parameter를 사용하지 않고, uri 경로만 이용한다
  ex] GET/static/star.jpg

### 동적 데이터 조회

- GET, query parameter를 사용해 데이터를 전달한다
  ex] GET /search?q=hello&hl=kr
- 검색이나 필터 사용시

### HTML Form 데이터 전송

- GET, POST만 지원한다

```html
<form action="/save" method="post">
  <input type="text" name="username" />
  <input type="text" name="age" />
  <button type="submit">전송</button>
</form>
```

- POST 사용시
  ![](https://images.velog.io/images/ouo_yoonk/post/68ee3e8d-32ce-4cac-99a0-81fe80af2789/image.png)

- GET 사용시
  ![](https://images.velog.io/images/ouo_yoonk/post/7c8c93f0-85a8-4647-876d-350d685a566e/image.png)

### HTML Form multipart

- POST

```html
<form action="/save" method="post">
  <input type="text" name="username" />
  <input type="text" name="age" />
  <input type="file" name="file1" />
  <button type="submit">전송</button>
</form>
```

![](https://images.velog.io/images/ouo_yoonk/post/f50c8706-c6c8-4498-9905-cd2e05adcbb0/image.png)

### HTTP API 전송

![](https://images.velog.io/images/ouo_yoonk/post/8c6c0297-7300-4479-8860-a41604b1805b/image.png)

- 서버 to 서버
- 앱 클라이언트
- 웹 클라이언트 : form 대신 ajax등
- Content-Type:application/json을 주로 사용한다. text, xml도 전송 가능하지만 json이 사실상 표준

---

**&#128209; reference**

- [인프런 - 모든 개발자를 위한 HTTP 웹 기본지식(김영한)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)
- [Wiki - REST](https://ko.wikipedia.org/wiki/REST)
