![](https://images.velog.io/images/ouo_yoonk/post/3ad2f482-4f0d-4618-aabd-4be96eceb8e3/%EC%95%B1%EC%9D%98_%EC%84%B1%EB%8A%A5%EA%B3%BC_%EC%82%AC%EC%9A%A9%EC%84%B1%F0%9F%98%8A.png)

# 성능 최적화와 사용성 개선을 위한 몇 가지 방법

## 성능 최적화

### 사이트 로딩 속도 개선

- tttb 측정
- 렌더링 횟수 줄이기
- 자바스크립트 번들 사이즈 줄이기 (code splitting)

### 중복 호출 방지

- api 중복 호출 방지
- 오류가 나지 않도록 api 호출 전후처리 꼼꼼히
- loading 액션등을 이용

### 이미지 지연 로딩 처리

- 이미지 리사이징해서 저장하기
- 여러 갈래로 저장
- .webp로 확장자를 바꾸어 저장하기
- 작은 이미지 가져다 쓰기
- css로 image sprite하기. 한 개의 이미지 파일로 만들어 background-position, background-image 속성을 이용

## 사용성 개선

보기 안좋은 것은 감추고, 불편한 것은 고치기!

### 이미지 지연 로딩

- 이미지가 100% 로딩된 후에 이미지를 보여주기

### 스피너, placeholder

### 에러 페이지 만들기

### validation 미리 체크

## 성능 지표 보기

### webVitlas

- 웹 사이트의 성능 지표를 확인할 수 있는 package

```javascript
// reposrtWebVitals.js
const reportWebVitals = (onPerfEntry) => {
  if (onPerfEntry && onPerfEntry instanceof Function) {
    import('web-vitals').then(({ getCLS, getFID, getFCP, getLCP, getTTFB }) => {
      getCLS(onPerfEntry); // Cumulative Layout Shift
      getFID(onPerfEntry); // First Input Delay - 웹페이지 반응성
      getFCP(onPerfEntry); // First Contentful Paint - 화면이 그려질 때까지 걸리는 시간
      getLCP(onPerfEntry); // Largest Contentful Paint - 화면에서 가장 큰 덩어리(중요도가 높은)를 로딩하는 데 걸리는 시간
      getTTFB(onPerfEntry); //  TIme To First Byte - 첫 번째 바이트를 가지고오는 데 걸린 시간
    });
  }
};

export default reportWebVitals;
```

```javascript
// index.js
...
reportWebVitals(console.log);
...
```

### firebase analytics

```javascript
// firebase.js
import "firebase/anaytics";
...
const analytics = firebase.anaytics();

```

```javascript
// index.js
import { analytics } from '../shard/firebase';

function sendToAnalytic(metric) {
  const _report = JSON.stringify(metric);

  analytics.logEvent('web_vital_report', _report);

  console.log({ _report });
}

reportWebVitals(sendToAnalytic);
```

## 렌더링 횟수 줄이기

- 성능 지표를 개선할 수 있는 가장 우선적인 방법

### React.memo

- 부모 컴포넌트가 바뀔 때마다 바뀔 게 없는 컴포넌트는 렌더링을 막아주는 방법
- 컴포넌트를 렌더링하고, 결과를 메모이제이션해둠
