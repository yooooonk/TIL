![](https://images.velog.io/images/ouo_yoonk/post/5ee10c51-c15a-4163-bf0b-96a718005d7e/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C_%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD%EC%9D%98_%EC%9D%B4%ED%95%B4%EC%99%80_%EC%8B%A4%EC%8A%B5_%5B%EA%B9%80%EC%A0%95%ED%99%98%EB%8B%98%5D__n_-_Node.js.png)

# 프론트엔드 개발에 Node.js가 필요한 이유

### 최신 스펙으로 개발할 수 있다.

- 자바스크립트의 발전에 비해 브라우저의 지원 속도는 느리기 때문에 babel 같은 도구가 필요함
- 웹팩, npm 같은 노드 기술로 만들어진 환경에서 사용할 때 비로소 자동화된 프론트엔드 개발환경을 갖출 수 있음
- typescript, sass 같은 고수준 프로그래밍 언어를 사용하려면 node.js 환경에서 돌아가는 전용 트랜스파일러가 필요함 --- 맞아?

### 빌드 자동화

- 파일 압축, 코드 난독화, 폴리필 추가 등의 작업을 거친후 배포
- 라이브러리 의존성을 해결하고, 각종 테스트를 자동화

### 개발 환경 커스터마이징

- react의 CRA나 Vuejs의 vue-cli를 사용할 수 없는 경우에 환경을 직접 커스터마이징 할 수 있다.

# 프로젝트 생성

`$ npm init`

![](https://images.velog.io/images/ouo_yoonk/post/f8d8eb2b-1dbf-4696-ad42-5fd134b7d86d/image.png)

- 프로젝트 폴더에 `package.json` 파일이 생김

```javascript
// package.json
{
  "name": "front-end-env",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

- script : - 프로젝트 자동화 쉘 스크립트

## 명령어

![](https://images.velog.io/images/ouo_yoonk/post/bf811d22-775b-4839-82fb-eb358f12c1be/image.png)
`$ npm <command>`

### 일반적으로 사용하는 명령어

- start : 어플리케이션 실행
- test : 테스트
- install : 패키지 설치
- uninstall : 패키지 삭제

### 커멘드 추가

- scripts 내부에 커멘드를 추가
- `$ npm run 추가한command` 로 실행

예) 아래와 같이 build 스크립트를 추가하고 `$ npm run build`
![](https://images.velog.io/images/ouo_yoonk/post/b299b5ac-9763-4e32-a6b5-22162748faf3/image.png)

# 패키지 관리

## CDN

```html
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
```

- Contents Delivery Network : 콘텐츠 전송 네트워크
- CDN으로 제공하는 라이브러리를 직접 가져 오는 방식. 주소를 html에서 로딩한다.
- CDN 서버 장애로 라이브러리를 사용할 수 없게될 수 있다.

## 직접 다운로드

- 라이브러리 코드를 프로젝트 폴더에 직접 다운로드 받는 방식
- CDN을 사용하지 않기 대문에 장애와 독립적으로 웹 어플리케이션을 제공할 수 있다.
- 버전관리의 어려움

## npm

`$ npm install 라이브러리`

- 라이브러리를 어느 한 곳에서 업데이트하고 하위 호환되는 안전한 버전만 다운받아 사용
- package.json에 dependencies에 추가됨
  ![](https://images.velog.io/images/ouo_yoonk/post/667450c7-c8d1-474e-96ed-b527bef9c9b3/image.png)

### nodejs가 버전을 관리하는 방식 - sementic version(유의적 버전)

`^주 버전.부 버전.수 버전`

ex] ^16.12.0

- 주 버전(Major version) : 기존 버전과 호환되지 않게 변경한 경우
- 부 버전(Minor version) : 기존 버전과 호환되면서 기능이 추가된 경우
- 수 버전(Patch version) : 기존 버전과 호환되면서 버그를 수정한 경우

### 틸트(~)와 캐럿(^)

- 틸트는 마이너 버전이 명시되어 있으면 패치버전을 변경한다.
  - ~1.2.3표기는 1.2.3부터 1.3.0미만 까지를 포함한다
    - ~0 표기는 0.0.0부터 1.0.0 미만 까지를 포함한다.
    - 하위 호환성을 지키지 못하는 버전으로 업데이트 될 수 있음
- 캐럿은 정식버전에서 마이너와 패치 버전을 변경한다.
  - ^1.2.3 표기는 1.2.3부터 2.0.0미만 까지를 포함한다.
    - 정식버전 미만인 0.x 버전은 패치만 갱신한다.
    - ^0 표기는 0.0.0부터 0.1.0미만까지를 포함한다.
    - 하위 호환성을 유지할 수 있다.

---

**&#128209; reference**

- [김정환 - 프론트엔드 개발환경의 이해:NPM](https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html)
- [갓대희의 작은공간 - CDN이란](https://goddaehee.tistory.com/173)
