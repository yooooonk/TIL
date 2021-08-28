![](https://images.velog.io/images/ouo_yoonk/post/913e9125-f306-4553-8e67-b176b6116513/Event2.png)

## 이벤트 핸들링
DOM의 모든 element는 event target을 상속한 node다. `Event target`은 DOM 인터페이스로, 이벤트를 받을 수 있고, 이벤트에 대한 리스너를 가질 수 있다. 이벤트가 발생하면 `event object`를 만들어서 등록한 콜백함수에 전달한다.

|method|action|
|--|--|
|`addEventListner`|특정한 이벤트에 event handler를 등록. 여러번 호출하면 핸드러를 여러개 붙일 수 있다.|
|`removeEventListner`|Event target에 등록된 이벤트 리스너를 제거|
|`dispatchEvent`|Event target에 이벤트를 발생시킴|

## Event object(이벤트 객체)
> 이벤트에 관한 상세한 정보를 가지고 있는 객체

이벤트가 발생하면 브라우저는 `이벤트 객체`라는 것을 만들어 핸들러 함수에 인수 형태로 전달한다.

|property||
|--|--|
|event.type|발생한 이벤트의 종류|
|event.currentTarget|이벤트를 처리하는 요소. 화살표 함수를 사용했거나 함수를 다른 곳에 바인딩한 경우에 이벤트가 처리되는 요소 정보를 얻을 수 있다.|
|event.target|이벤트가 발생한 가장 안쪽의 요소|



## 버블링과 캡처링
DOM 이벤트에서 정의한 이벤트 흐름 3단계

![](https://images.velog.io/images/ouo_yoonk/post/eaf42b84-71a0-4d93-98e9-0df49f633647/image.png)

1. 캡처링 - 이벤트가 하위 요소로 전파
2. 타깃 - 이벤트가 실제 타깃 요소에 전달되는 단계
3. 버블링 단계 - 이벤트가 상위 요소로 전파되는 단계

### 캡처링 Capturing
최상위 조상에서 이벤트가 시작해 아래로 전파되는 단계이다. 캡처링 단계를 이용해야 하는 경우는 흔치 않다.

### 버블링 Bubbling
자식 요소에서 이벤트가 발생하면 부모 요소까지 이벤트가 전파되는 것을 말한다. 즉 한 요소에 이벤트가 발생하면, 부모 요소의 등록된 핸들러가 동작한다. 가장 최상단의 조상 요소까지 이 과정을 반복하면서 요소 각각에 할당된 핸들러가 동작한다. 거의 모든 이벤트는 버블링되지만 `focus` 이벤트와 같이 버블링 되지 않는 이벤트도 있다.

- `event.target` : 실제 이벤트가 시작된 요소. 버블링이 진행되어도 변하지 않는다.
- `event.currentTarget` : '현재' 요소. 현재 실행 중인 핸들러가 할당된 요소(=this)

버블링을 중단하기 위해서 `event.stopPropagation()`을 사용할 수 있지만 꼭 필요한 경우가 아니면 사용하지 않는게 좋다. 클릭 이벤트를 분석하기 위해 이벤트 리스너를 등록해둔 경우, stopPropagation을 사용하면 분석 로직이 동작하지 않을 수 있다.
이벤트 핸들러가 원하는 상황에서만 동작하도록 코드를 작성하는 것이 더 좋다.

``` javascript
const addButton = document.querySelector('.add-button')
const buttonParent = document.querySelector('.parent-div')

buttonParent.addEventListner('click',(e)=>{
	if(e.currentTarget !== e.target){
    	return;
    }
  
  	console.log('div 이벤트')
})

addButton.addEventListner('click',(e)={
	console.log('버튼 클릭')
})
```


## 이벤트 위임
비슷한 방식으로 여러 요소를 다뤄야 할 때, 각각의 자식요소에 이벤트를 할당하지 않고, 공통 조상에 이벤트 핸들러를 할당해 여러 요소를 다룰 수 있다. 성능면에서도 이 방법이 더 좋다. 

각 요소에 이벤트 할당
``` html
<ul>
	<li>우유</li>
  	<li>두유</li>
  	<li>커피</li>
</ul>
```
``` javascript
const items = document.querySelectAll('li')

items.forEach(item=>{
	item.addEventListner('click',onClickItem)
})

const onClickItem = (e)=>{
	console.log(e.innerText)
}
```

이벤트 위임
``` javascript
const list = document.querySelector('ul')

list.addEventListner('click',onClickItem)

const onClickItem = (e)=>{
	if(e.target.tagName === 'li'){
    	console.log(e.target.innerText)
    }
}
```

## 이벤트의 기본 동작
많이 이벤트가 발생 즉시 브라우저에 의해 특정 동작을 자동으로 수행한다.

- a 태그 : 링크를 클릭하면 해당 URL로 이동
- submit : 서버에 form 데이터가 전송

자바스크립트를 사용해 직접 동작을 구현해야하는 경우 기본적인 동작을 막는 방법은 두 가지다.
- `event.preventDefault()` 메서드를 사용
- addEventListner가 아닌 on<event> 방식으로 할당되었다면 false를 반환
``` html
 	<a href='/' onclick="return false">하이</a>	
```

addEventLister의 `passive:true` 옵션은 브라우저에게 preventDefault()를 호출하지 않겠다고 알리는 역할을 한다. 예를 들어 모바일 기기에서 touchmove와 같은 이벤트는 스크롤링을 발생시키는데 `preventDefault()`를 사용하면 스크롤링을 막을 수 있다. 브라우저는 스크롤링을 발생시키는 이벤트를 감지했을 때 모든 핸들러를 처리하는데, preventDefault가 어디에서도 호출되지 않은 것을 확인하고 스크롤링을 진행한다. 이 과정에서 지연과 버벅임이 발생하는데 `passive:true` 옵션을 주면 핸들러가 스크롤링을 취소하지 않을 것이라는 정보를 브라우저에게 알려줘서, 브라우저는 화면을 최대한 자연스럽게 스크롤링을 처리할 수 있다. passive 옵션은 기본적으로 정해져있기 때문에 임의로 조작하지 않는 편이 좋다.
  

## 기타 
- `keypress` 타입은 deprecated
- `keydown` 이벤트는 브라우저가 입력을 처리하기 전에 발생, `keyup` 이벤트는 브라우저가 입력을 처리한 후에 발생
- `form`을 이용하면 여러 input의 value를 한번에 받아올 수 있다

---
__📑 referece__
- [MDN - event target](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)
- [모던 javascript](https://ko.javascript.info/introduction-browser-events#ref-121)

