## CSS Layout
- 엘리먼트를 화면에 배치하는 것
- 엘리먼트는 위에서 아래로 순서대로 블럭을 이루며 배치되는 것이 기본
### 주요 속성
- __display__ (block, inline, inline-block)
    - block : 벽돌처럼 블록을 가지고 쌓임
    - inline : 옆으로 흐름. 
    - inline-block    
    ![block](https://github.com/yooooonk/TIL/blob/master/img/display.PNG)

- __position__ (static,absolute,relative,fixed)
    - static : 기본값, 순서대로 배치
    - absolute : 상위 엘리먼트 중 position이 static이 아닌 것을 기준점으로 top/left/tight/bottom으로 설정
    - relative : 원래 자신이 위치해야 할 곳을 기준으로 상대적인 값을 부여 top/left/right/bottom
    - fixed : 전체화면 좌측, 맨위를 기준으로, 스크롤을 해도 그 위치 그대로 
    ![position](https://github.com/yooooonk/TIL/blob/master/img/position.PNG)
- __float__ (left,right) : 원래 flow에서 벗어나 둥둥 떠다닐 수 있다, 좌우배치가 가능
    ![float](https://github.com/yooooonk/TIL/blob/master/img/float.PNG)
- __box-model__
    ![box-model](https://github.com/yooooonk/TIL/blob/master/img/box-model.png)
    - 전체 / 위아래 좌우 / 위 오른쪽 아래 왼쪽
    - Margin : 엘리먼트 간의 간격
    - Border : 테두리. 두께를 조절해 간격처럼 보일 수 있음
    - Padding
- __box-sizing__
    - content-box : 기본값, padding 값에 따라 박스 크기가 달라짐
    - border-box : padding을 줘도 박스크기 고정
    ![box-sizing](https://github.com/yooooonk/TIL/blob/master/img/box-sizing.PNG)


## div vs span
- span : inline-level
- div : block-level
- display
    - inline
    - inline-block
    - block
![div](https://github.com/yooooonk/TIL/blob/master/img/div_display.PNG)
![span](https://github.com/yooooonk/TIL/blob/master/img/span_display.PNG)
---
__reference__
- [드림코딩 by 엘리 - CSS 레이아웃 정리 display, position완성](https://www.youtube.com/watch?v=jWh3IbgMUPI&t=36s)