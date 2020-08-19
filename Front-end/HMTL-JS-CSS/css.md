# CSS

## 문법
```css
selector {
    property : value
}
```

## style을 HTML 페이지에 적용하는 3가지 방법
### 1. inline
- HTML 태그 안에
- 같은 속성을 추가하려고 할때 가장 우선순위가 높음

```html
<p style="border:1px solid gray;color:red;font-size:2em;">
```
### 2. internal
- style 태그로 지정
- 구조와 스타일이 섞여 유지보수가 어렵다
- 별도의 CSS파일을 관리하지 않아도 되고, CSS 파일을 부르기 위해 별도이 필요없음
``` html
<head>
<style>
p  {
  font-size : 2em;
  border:1px solid gray;
  color: red;
}
</style>
</head>

<body>
<div>...</div>
</body>
```
### 3. external
- 외부파일(.css)로 지정하는 방식
- 가급적 이 방법으로 할 것을 추천
- link태그로 추가해서 사용
``` html
<html>
	<head>
		<link rel="stylesheet" href="style.css">
	</head>
	<body>
		<div>
			<p>
				<ul>
					<li></li>
					<li></li>
					<li></li>
					<li></li>
				</ul>
			</p>
		</div>
	</body>
</html>
```

## CSS 상속
- 상위에서 적용한 스타일은 하위에도 반영됨
- box-model 속성(padding,border,width,height,margin)과 같은 크기와 배치 관련된 속성은 예외
- block element의 크기는 기본적으로 부모의 크기만큼을 가짐

## 선택자 우선순위
- 선언방식에 따른 차이 : inline > internal > external
- 구체적으로 표현된 것이 있다면 먼저 적용
- id > class > element

## Selector
- 태그 : 태그명
- id : #id
- class : .class
```html
<style>     
     #spantag {
       color : red;
     }
     .spantag{
         color : red;
     }

     span {
         color : red
     }
</style>

<body>
     <span id="spantag"> HELLO World! </span>
     <span class="spantag"> HELLO World! </span>
     <span> HELLO World! </span>
</body>
```

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


---
- [edwith 부스트코스 웹 프로그래밍](https://www.edwith.org/boostcourse-web/lecture/16668/)