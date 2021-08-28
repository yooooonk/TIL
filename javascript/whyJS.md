# Java Script
- 웹 Frontend에 쓰이는 유일한 프로그래밍 언어
- 유일한 웹언어이기 때문에 발전이 빠르다
- interactive한 웹사이트, 웹앱, 모바일 앱, 데스크톱 앱을 만들 수 있다
- ECMAScript : 자바스크립트 표준
    - 각 브라우저는 ECMAScipt Specification을 받아 각자의 방식으로 작동시킴
- Vanila JS :  JS without library

## Variable
- let : 값을 바꿀 수 있다
- const : 상수, 변경 불가능, 변수 선언은 기본적으로 const로 하는 것을 권장
- var : 값을 바꿀 수 있다, global variable
- camelCase

## Data type
- String : 문자열, ""
- Boolean :  true, false 
- Float : 소수점

## Array []
```javascript
const daysOfWeek = ['Mon','Tue','Wed','Thu','Fri','Sat','Sun', true]

console.log(daysOfWeek)
```

## Object {}
``` javascript
const info = {
    name : "ouo",
    age : 29,
    gender : "Female",
    inandsome:true
}

console.log(info.name); // ouo

info.age = 30;

console.log(info.age);//30
```

### DOM
- Document Object Module
- 자바스크립트는 html 태그를 가져와서 object로 바꿈

### Local storage
- 자바스크립트 정보를 저장

---
__reference__
- [바닐라 JS로 크롬 앱 만들기-nomad coder](https://nomadcoders.co/javascript-for-beginners/lobby)