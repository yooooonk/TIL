# Event

## 이벤트 핸들링
- 특정 요소에 event 핸들러를 등록(모든 element는 이벤트 타겟임)
- 이벤트가 발생하면 event object를 만들어서 등록한 콜백함수에 전달
- addEventListner
- removeEventListner
- dispatchEvent : 이벤트를 발생시킴

## 버블링과 캡처링
- 캡처링 : 부모컨테이너에 등록된 이벤트가 자식으로 내려오는 거
- 버블링 : 자식컨테이너에 등록된 이벤트가 실행되면서 부모 컨테이너의 이벤트까지 실행되는거 
    - event.stopPropagation()으로 버블링을 방지하지만, 가능한 안 쓰는게 좋다.
    - 내가 관심있는 이벤트만 처리하도록 if문으로 처리하는 걸 권장.
- event.preventDefault()
## 이벤트 위임
- 부모 요소는 자식요소에서 발생하는 모든 이벤트를 들을 수 있다.
- 자식요소 하나하나에 이벤트를 등록하는 것 보다 부모 요소에 등록해 event.target으로 구분해 이벤트를 거는게 좋다

## keyup과 keydown
- keydown은 브라우저가 입력을 입력하기 전에 이벤트 실행
- keyup은 입력을 처리한 후 이벤트 실행

## web form
- 폼 태그 안에 폼 value를 한번에 받아올 수 있음