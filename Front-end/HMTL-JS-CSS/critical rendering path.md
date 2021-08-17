# Critical rendering path

- requests/response -> loading -> scripting -> rendering -> layout -> patining

DOM->CSSOM->RenderTree -> layout->paint->composition
--------------------      ------------------------
Construction                    Operation
- Construction : DOM 요소, CSS 요소가 작을수록 렌더트리를 빨리 만들 수 있음(불필요한 tag, div 남용, 불필요한 래핑요소 ㄴㄴㄴ)
- Operation : paint가 자주 일어나지 않도록 하는 것이 중요. ex. translate의 경우 레이어의 위치만 바꾸기 때문에 paint가 다시 발생하지 않음. layout이 바뀌는경우 성능이 나빠진다. 애니메이션 transition을 이용할 떄 어떤 속성값, 어떤 CSS를 쓰느냐에 따라 layout - paint - composition이 다르게 발생할 수 있다.
- 예를들어 움직일 때는 top, left를 쓰면 layout+paint+composition이 다 발생하지만 translate를 이용할 경우 composition만 발생한다. 

- layout : CSS 스타일이 포함. x,y,너비, 높이 등을 계산
- paint(중요) : 레이어 단위로 준비(z-index 등). 변화가 있을 때 해당 레이어만 수정하면 되므로 성능상 이점이 있다. 
- composition : 준비한 레이어를 브라우저 위에 놓음
