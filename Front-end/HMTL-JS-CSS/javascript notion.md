# Javascript 핵심개념

## 기본형과 참조형의 종류 및 차이점
- 기본형(Privitive Type) : Number, String, Boolean, null, undifined = 값을 그대로 할당
    |변수명|주소|데이터|
    |---|---|---|
    |a|@123|123|
- 참조형(Reference Type) : Object(array, Function, RegExp) = 값이 저장된 주소값을 할당(참조)
    |변수명|주소|데이터|
    |---|---|---|
    |obj|@123|@1011|
    ```javascript
        var obj = { //@1011 -- a : @1012 b:@1013
            a : 1, // @1012
            b : 'b' //@1013
        }
    ```

## 함수
### 함수 호이스팅
- 변수선언, 함수 선언을 끌어올림

### 함수 선언문 vs 함수 표현식
- 할당을 하지 않으면 전체가 호이스팅되고(함수 선언문), 할당을 하면 변수만 호이스팅 되고 함수는 그 자리에 남아 있음(함수 표현식)
- 함수 선언을 하면 같은 이름으로 선언한 함수가 있을 경우 이전에 선언한 함수가 덮어쓰기 됨
- 가독성 측면에서도 함수 표현식을 사용하는 것을 권장

``` javascript

function 함수선언문(){
    return 'aa'
}

var b = function 기명함수표현식(){
    return 'bb'
}

var 익명함수표현식 = function(){
    return 'cc'
}
```

### 함수 스코프 vs 실행컨텍스트
- 스코프 : 정의될 때 결정
- 실행 컨텍스트 : 해당 함수를 실행할 때 필요한 정보를 담은 집합체, 실행될 때 생성, 호이스팅, this 바인딩 등으 ㅣ정보가 담긴다

### 콜백함수
- something will call this function back!
- 해당 함수의 제어권을 호출하는 함수가 가짐 -- bc함수의 제어권을 setInterval 함수가 가짐
- 같은 함수를 메서드로 사용하는지, 콜백함수로 사용하는지에 따라 this의 범위가 달라짐
```javascript
var bc = function(){
    console.log('1초마다 실행')    
}

setInterval(bc,1000)
```