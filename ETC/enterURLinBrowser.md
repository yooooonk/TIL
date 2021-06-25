![](https://images.velog.io/images/ouo_yoonk/post/b36ee16c-1ebe-40a3-ba47-9e530a0663a0/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80_%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90__n_URL%EC%9D%84_%EC%9E%85%EB%A0%A5%ED%95%98%EB%A9%B4__n_%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94_%EC%9D%BC_%F0%9F%8C%90.png)

### 1. 브라우저가 URL 해석

- scheme : 프로토콜://[user정보]host[포트]
- url scheme형식이 아니면 브라우저 기본 검색엔진으로 검색
- 맞으면 서버 요청

### 2. HSTS 목록 조회해, HTTPS 통신해야할지 HTTP 통신해야할지 확인

- HTTPS인지 HTTP인지 알려줌

### 3. URL을 IP로 변환

- 먼저 캐시를 확인 : 브라우저나 로컬에 저장된 도메인이 잇는지 확인
- 없으면 DNS에 요청 - DNS는 local Router, ISP의 캐싱 DNS

### 4. 라우터를 통해 해당 서버의 게이트웨이로 이동

- 라우터는 목적지의 최적 경로를 알려주는 장비
- 서로 다른 네트워크끼리 통신을 가능하게 함
- 라우팅 테이블이 경로 정보를 가지고 있음
- 게이트웨이 : 다른 네트워크로 들어가는 입구역할. 서로 다른 네트워크와 프로토콜끼리 통신이 가능하게 끔 함

### 5. IP주소를 MAC주소로 변환(ARP)

- ARP(Address Resolution Protocol) : 주소 해석 프로토콜
- 네트워크 스위치 장비가 ARP 요청을 받으면, 자신이 가지고 있는 MAC 테이블에서 반환
- MAC 주소가 필요한 이유는 IP는 논리주소고, 실제로 물리계층에서 동작하는 실제주소가 MAC 주소 - OSI 7계층에 따라 그렇게 약속함

### 6. 대상 서버와 TCP 소켓 연결 확립

- 3 way handshake + TLS handshake
- HTTPS는 80번, HTTP는 443번 포트

### 7. HTTP 프로토콜로 요청, 응답

### 8.브라우저가 파싱