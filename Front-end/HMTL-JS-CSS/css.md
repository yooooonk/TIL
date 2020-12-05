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

---
- [edwith 부스트코스 웹 프로그래밍](https://www.edwith.org/boostcourse-web/lecture/16668/)