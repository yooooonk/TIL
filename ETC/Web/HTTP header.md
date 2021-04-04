# 일반헤더

`header-field=field-name: field-value`

- 용도 : HTTP 전송에 필요한 모든 부가정보
- 필요시 임의의 헤더 추가 기능
- 헤더 분류

![](https://images.velog.io/images/ouo_yoonk/post/b9490886-a893-4c59-b34c-c12b8fd92a35/image.png)

| 분류            | 용도                                                                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| General header  | 메시지 전체에 적용되는 정보 ex)connection                                                                                                     |
| Request header  | 요청정보 ex)User-Agent:Mozilla                                                                                                                |
| Response header | 응답 정보 ex)Server:Apache                                                                                                                    |
| Entity header   | 엔터티 바디정보<br> --> Reresentagtion header(표현헤더)로 바뀜 - 표현 데이터를 해석할 수 있는 정보 제공. 데이터 유형, 데이터길이, 압축정보 등 |

## 표현헤더

| Header           | 용도                                                                                                                  | 예시                                      |
| ---------------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| Content-Type     | 표현데이터 형식-미디어타입, 문자인코딩                                                                                | text/html:charset=utf-8, application/json |
| Content-Encoding | 표현데이터 압축방식 <br/> 데이터를 전달하는 곳에서 압축 후 인코딩헤더 추가, 데이터를 읽는 쪽에서 헤더 정보로 압축해제 |
| Content-Language | 표현데이터 자연언어                                                                                                   | ko,en                                     |
| Content-Length   | 바이트 단위 길이                                                                                                      |                                           |

## 협상헤더 Content Nagotiation

- 클라이언트가 선호하는 표현 요청(요청시에만 사용)

| Field           | 용도        |
| --------------- | ----------- |
| Aeecpt          | 미디어타입  |
| Aeecpt-Charset  | 문자인코딩  |
| Aeecpt-Encoding | 압축 인코딩 |
| Aeecpt-Language | 자연언어    |

### 협상우선순위

1. Quality Values(q)
   `text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8`
2. 구체적인 것이 우선됨

## 일반정보

| Field      | 용도                                                                                                    |
| ---------- | ------------------------------------------------------------------------------------------------------- |
| From       | user-agent email정보, 잘 안 씀                                                                          |
| `Referer`  | 이전 웹 페이지주소 <br/> ex)구글에서 위키검색하면 referer:www.google.com로 표현 -> 유입경로 분석가능    |
| User-Agent | 클라이언트 애플리케이션 정보(웹 브라우저 등) <br/> 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능 |
| Server     | 요청을 처리하는 Origin 서버의 소프트웨어 정보                                                           |
| Date       | 메시지가 발생한 시간 - 응답시에만 사용                                                                  |

## 특별한 정보

| Field    | 용도                                                                                                                          |
| -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `Host`   | 필수헤더! 요청에서 사용 <br/>하나의 IP 주소에 여러 도메인이 적용되어 있을 때나 <br>하나의 서버가 여러 도메인을 처리해야 할 때 |
| Location | 응답코드가 300번이고 location 헤더가 있으면 페이지 리다이렉션                                                                 |

## 인증

| Field           | 용도                                                                         |
| --------------- | ---------------------------------------------------------------------------- |
| `Authorization` | 클라이언트 인증 정보를 서버에 전달한다 <br> 인증밥법에 따라 Barer , Basic 등 |

## 쿠키✨

![](https://images.velog.io/images/ouo_yoonk/post/56befad1-6172-4829-bc8f-c6b18a3b1023/image.png)

| Field      | 용도                                                               | 예시                                                                             |
| ---------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| Set-Cookie | 서버에서 클라이언트로 쿠키 전달(응답)                              | Set-Cookie: cookie-name=cookie-value; Expires=date (또는 Max-Age=non-zero-digit) |
| Cookie     | 클라이언트가 서버에서 받은 쿠키를 저장하고 HTTP 요청시 서버로 전달 |

- 사용처 : 로그인 세션관리, 광고 정보 트래킹 등
- 쿠키 정보는 항상 서버에 전송되므로 최소한의 정보만 사용(세션 id, 인증토큰)
- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지를 이용한다

# 캐시와 조건부 요청

## 캐시

- 캐시 가능 시간동안 네트워크를 사용하지 않아도 되므로 네트워크 사용량을 줄일 수 있다
- 브라우저 로딩 속도가 매우 빠르다
- 빠른 사용자 경험이 가능하다
- 캐시 유효기간이 초과하면 서버를 통해 데이터를 다시 조회하고 캐시를 갱신한다. 이 때 다시 네트워크를 다운로드한다
- 검증 헤더와 조건부 요청을 이용해 몇 가지 정보로 캐시 신선도를 판단한다
- `Last-Modified(최종스정일 - 검증 헤더)`와 `if-modified-since(조건부요청)`를 이용해 수정된게 없으면 HTTP body를 전송하지 않는다

### 검증헤더

- ETag
- Last-modified

### 조건부 요청헤더

- If-Match -- If-Modified-since
- If-Nne-match -- If-Unmodifired-since

### 캐시 지시어

- max-age
- no-cache : 데이터는 캐시해도 되지만, 항상 원서버에 검증하고 사용
- no-store : 민감한 정보이므로 저장하지 않는다. 메모리에서 사용하고 최대한 빨리 삭제

---

**&#128209; reference**

- [인프런 - 모든 개발자를 위한 HTTP 웹 기본지식(김영한)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)
- [MDN - HTTP헤더](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)
