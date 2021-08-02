# Web APIs

[MDN - Web APIs](https://developer.mozilla.org/ko/docs/Web/API)

## 종류 
- DOM APIs
- Network APIs
- Graphics APIs
- Audio/Video APIs
- Device APIs
- File APIs
- Storage APIs
등등등

## 브라우저 구조분석
![](https://images.velog.io/images/ouo_yoonk/post/389d746a-5086-4b03-bfb5-eab4301f7207/image.png)
- `문서 객체 모델(Document Object Model, DOM)` : 웹 페이지 내의 모든 콘텐츠를 객체로 나타내준다. `document` 객체는 페이지의 기존 진입점 역할을 한다.
- `브라우저 객체 모델(Browser Object Model, BOM)` : 문서 이외의 모든 것을 제어하기 위해 브라우저(호스트 환경)이 제공하는 추가 객체를 나타낸다.
    - `navigator` : 브라우저와 운영체제에 대한 정보를 제공한다.
    - `location` : 현재 URL을 읽을 수 있게 해주고 새로운 URL로 변경할 수 있다.

## 브라우저의 좌표  
![](https://images.velog.io/images/ouo_yoonk/post/78782879-eacf-4eab-81f6-9b64fb34b1cf/image.png)
### getBoundingClientRect
- `element.getBoundigClientRect()` 메서드는 `elem`을 감싸는 가장 작은 네모의 창 기준 좌표를 DOMRect 클래스의 객체 형태로 반환한다.

- `x와 y` : 요소를 감싸는 네모창 기준 x,y
- `width와 height` : 요소를 감싸는 네모의 너비, 높이

- 창 기준 : `clientX`  `clientY`

- 문서 기준 : `pageX` `pageY`

---
__reference__
- 모던 자바스크립트 튜토리얼(브라우저 환경과 다양한 명세서)
- 모던 자바스크립트 튜토리얼(좌표)