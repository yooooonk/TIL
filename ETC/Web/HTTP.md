![](https://images.velog.io/images/ouo_yoonk/post/449b912b-0205-498e-a37f-59671d1a281d/HTTP%F0%9F%93%9C.png)

# HTTP

> HTTP는 월드 와이드 웹에 내재된 프로토콜. Tim Berners-Lee에 의해 1989년부터 1991년에 발명된 HTTP는 본래의 **단순함**의 대부분을 지키면서 확장성 위에서 만들어지도록, 많은 수정을 거쳐왔다. HTTP는 의사-신뢰도가 있는 실험실 환경에서 파일을 교호나하는 프로코톨에서 높은 수준의 분석과 3D 내에서 이미지와 비디로를 실어나르는 현대 인터넷 정글로 진화해 왔다.

원래는 HyperText Transfer Protocol, 즉 html을 전송하는 프로토콜이었으나, 요즘에는 html, text,image, 음성, 영상, 파일 등 거의 모든 형태의 데이터를 전송한다.

| 버전       | 특징                                                                                                                                                      |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP/0.9   | GET 메서드만 지원                                                                                                                                         |
| HTTP/1.0   | 메시지, 헤더추가                                                                                                                                          |
| HTTP/1.1✨ | 표준 프로토콜, 현재 사용하는 대부분의 기능 포함                                                                                                           |
| HTTP/2.0   | 2015년. 성능개선                                                                                                                                          |
| HTTP/3.0   | TCP 대신 UDP를 사용,애플리케이션 레벨에서 성능을 최적화 할 수 있도록 새로 설계해서 나온것 [더보기](https://evan-moon.github.io/2019/10/08/what-is-http3/) |

# HTTP의 특징

## 1. 클라이언트-서버구조

![](https://images.velog.io/images/ouo_yoonk/post/3e20a3a7-e426-49cb-9a63-c49185344fbc/image.png)

- request-response 구조
- 클라이언트는 서버에 요청을 보내고 응답을 대기
- 서버는 요청에 대한 결과를 만들어서 응답
- **클라이언트는 UI와 사용성을 담당하고, 서버는 비즈니스 로직을 담당해 각각 독립적으로 진화할 수 있다.**

## 2. 무상태성 stateless

- 서버가 클라이언트의 상태를 보존하지 않는다
- 모든 것을 무상태로 설계할 수는 없이 때문에(로그인 등) 상태유지가 필요할 때는 브라우저 쿠키와 서버 세션 등을 이용한다.

### 장점

- 응답서버를 쉽게 바꿀 수 있기 때문에 서버 확장성이 높다(scale out).
- 클라이언트 요청이 증가해도 서버 증설만 하면 아무 서버와 통신이 가능하고, 서버 장애가 생겨도 다른 서버와 통신할 수 있다.

### 단점

-클라이언트가 필요한 데이터를 다 담아서 요청해야한다.

## 3. 비연결성 connectionless

- 연결을 지속적으로 유지하면 서버 자원을 모소한다.
- http는 요청 응답을 받으면 바로 TCP/IP 연결을 끊어 서버 자원을 최소한으로 사용한다

### 장점

- 서버 자원의 효율적인 사용
- 일반적으로 초단위 이하의 빠른 속도로 응답하기 때문에 한시간동안 수천명이 사용해도 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 적다

### 단점

- TCP/IP 연결을 새로 맺어야 하므로 3 way handwake 시간이 추가된다
- 웹브라우저로 사이트를 요청하면 수많은 자원(html, 이미지, javascript 등)을 받기 위해 여러번 연결을 해야한다
- 그래서 요즘은 html 파일을 완저히 다 받을 때까지 연결을 유지한다(지속연결)

# HTTP 메시지

## 구조

![](https://images.velog.io/images/ouo_yoonk/post/c3866425-a3e2-4816-8242-dcd2db19b8f5/image.png)

![](https://images.velog.io/images/ouo_yoonk/post/9b9bceb6-8527-4b94-8e5c-a12373da3ee0/image.png)

### start-line

- request line(요청시)
  `GET /search?q=hello&hl=ko HTTP/1.1` - `method` SP `reqeust-target` SP `HTTP-version` CRLF - method : http 메서드 - reuqest-target : 요청대상 - http version
- status line(응답시)
  `HTTP/1.1 200 OK` - `http version` sp `status-code`sp`reason phrase`

### 헤더

- HTTP 전송에 필요한 모든 부가정보
- 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 정보, 캐시 관리 정보, ... [표준헤더 더보기](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
- 임이의 헤더도 추가 가능하다
- `field-name:value`
  ex] Host:value -- request
  Content-Type: text/html;charset=UTF-8

### empty line

### 메시지바디

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송가능

---

**&#128209; reference**

- [인프런 - 모든 개발자를 위한 HTTP 웹 기본지식(김영한)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)
- [MDN HTTP의 진화](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
- [HTTP/3는 왜 UDP를 선택한걸까](https://evan-moon.github.io/2019/10/08/what-is-http3/)
