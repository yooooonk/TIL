![](https://images.velog.io/images/ouo_yoonk/post/d469bd99-163f-45d3-a7e2-9c510c5ac4a3/CRP_n(Critical_Rendering_Path).png)

# Critical rendering path

> 브라우저가 HTML, CSS, Javascdript를 화면에 픽셀로 변환하는 일련의 단계

![](https://images.velog.io/images/ouo_yoonk/post/ae3a0158-0a4e-44f2-842b-f30712c612cf/image.png)

CRP는 DOM, CSSOM, Render tree, Layout, Paint를 포함한다. CRP를 이해하고 최적화하는 것은 뛰어난 사용자 상호작용을 보장하며 버벅거림을 피할 수 있도록 하고, `1초당 60프레임`에 리플로우와 리페인트가 발생할 수 있도록 하는데 중요하다. 

브라우저는 요청 후에 서버로부터 HTML을 응답받는다. 응답받은 HTML을 분석하고, 수신된 바이트를 `DOM트리`로 변환한다. 브라우저는 스타일시트, 스크립트 또는 외부 자원(이미지 참조 등)에 대한 링크를 찾을때마다 요청을 한다.(불러온 에셋을 다룰 때까지 나머지 HTML을 분석 작업은 중단됨) CSSOM이 완료되면 브라우저는 렌더 트리를 생성하고 보여지는 컨텐츠를 위해 스타일을 계산한다. 렌더트리가 완료된 후 모든 렌더 트리 요소들에 대한 위치와 크기가 정의된 레이아웃이 만들어진다. 

|Construction|Operation|
|--|--|
|`DOM`->`CSSOM` -> `Render Tree` |`Layout` -> `Paint` -> `Composition`|

## 1. DOM
![](https://images.velog.io/images/ouo_yoonk/post/dcd7a4de-afce-41b9-a5ee-63e28411e90a/image.png)

- DOM Tree는 완전하게 파싱된 HTML 페이지의 Object 표현이다.
- html로부터 시작해 각 element, text에 대한 `node`가 만들어진다.
- DOM Tree 생성은 점진적으로 진행된다. 페이지에 내용을 표시하기 위해 문서 전체를 로드할 필요가 없다.
- CSS와 javascript 로드시에 페이지의 렌더링을 차단할 수 있다.
- 불필요한 tag나 wrapper는 사용하지 않고, div를 남용하는 대신 sementic 태그를 이용하는 것이 성능에 좋다.

## 2. CSSOM
![](https://images.velog.io/images/ouo_yoonk/post/0b680a5d-793c-4708-9fc9-7f4912730e1e/image.png)

- DOM을 스타일링 하기 위한 페이지의 모든 스타일 정보
- CSS는 상속과 덮어쓰기가 가능하기 때문에 CSS 전체가 파싱되기 전에 사용하면 잘못된 스타일이 적용될 수 있다. 
- 따라서 브라우저는 모든 CSS를 수신하고 처리할 때까지 페이지 렌더링을 막는다.
- 구체적인 선택자보다 덜 구체적인 선택자가 더 빠르지만 성능차이가 크지는 않다. 

## 3. Render Tree 만들기
![](https://images.velog.io/images/ouo_yoonk/post/6c84be23-6eea-40a4-88ee-1999198133a9/image.png)

- DOM과 CSSOM이 합쳐진 것으로 페이지에서 최종적으로 렌더링할 내용을 나타내는 Tree
- Render Tree는 오직 보여지는 node만 캡쳐한다. 
	- 예] display:none 속성은 렌더트리에 포함되지 않는다.(visible:hidden은 포함됨)

## 4. Layout

- 요소들이 페이지에서 배치되는 위치와 방법, 각 요소의 `너비`와 `높이` 그리고 서로 관련된 `위치`를 결정한다.
- 뷰포트 메타 태그는 레이아웃의 너비를 정의한다.
``` html
<meta name="viewport" content="width=device-width, initial-scale=1">
```
- 레이아웃은 디바이스가 회전하거나 브라우저의 사이즈가 조정될 때마다 발생한다.
- 레아아웃의 성능은 DOM의 영향을 받는다. 노드의 수가 많을수록 레이아웃은 더 길어지며, 스크롤링 또는 다른 애니메이션이 있으면 레이아웃에 jank를 일으키는 병목현상이 발생할 수 있다.
- 레아아웃 이벤트의 반복과 형성시간을 줄이기 위해서 일괄 업데이트를 해야하고, 박스 모델 속성을 애니메이션화 하지 말아야 한다. 
- 박스모델 : HTML 요소를 padding, border, margin, content 으로 구분하는 것.

## 5. Paint
- 화면에 픽셀을 그리는 단계. 
- 렌더 트리가 생성되고 레이아웃이 나타나기 시작하면 화면에 픽셀을 그릴 수 있다.
- load시에 전체 화면을 그리고, 이후에는 브라우저가 필요한 최소 영역만 다시 그리도록 최적화 되어있다
- `Layer 단위`로 준비(z-index 등). 변화가 있을 때 해당 레이어만 수정하도록 최적화되어 있다.

## 6. Composition
- 준비한 레이어를 화면에 놓는 과정

## CRP 최적화 방법
- 자원 로드 순서 관리
- 파일 사이즈 줄이기
- 자원 다운로드를 연기함으로써 중요 자원들의 수를 최소화
- Operation 과정에서 layout, paint는 되도록 적게 발생해야 함
	ex] element를 이동할 때 top, left 속성을 변경하면 layout+paint+composition이 다 발생하지만 translate를 이용할 경우 composition만 발생한다.
https://csstriggers.com/ 참고

---
__📑 referece__
- [MDN - 중요 렌더링 경로](https://developer.mozilla.org/ko/docs/Web/Performance/Critical_rendering_path)
- https://bitsofco.de/understanding-the-critical-rendering-path/
- [Woonism Ciritical Rendering Path란](https://wonism.github.io/critical-rendering-path/)