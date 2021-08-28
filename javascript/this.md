# this

- **호출한 주체**에 대한 정보가 담긴다!!! 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수!!!!
- 바인딩 : 식별자와 값을 연결하는 과정. this binding은 this가 가리킬 객체를 바인딩하는 것!
- 함수를 어떤 방식으로 호출하느냐에 따라 this의 값이 달라진다!!!! this는 함수를 호출할 때 결정된다.

## this binding

- **전역객체**의this는 = window
- **메서드 : 자신을 호출한 대상 객체에 관한 동작을 수행한다.    .xxx가 메서드**
    - this는 자신을 호출한 **대상 객체**
- **함수** 로 호출할 때는 this가 **전역객체**
- 해당 함수를 호출하는 구문 앞에 점 또는 대괄호 표기의 여부가 this 바인딩을 결정하는 유일한 조건이다.
- **화살표함수** 는 실행 컨텍스트를 생성할 때 this를 바인딩하지 않고, 상위 스코프의 this를 그대로 활용
- **콜백함수** 도 기본적으로 this가 전역 객체를 참조한다. addEventListner 는 .앞의 부분이 this 바인딩. forEach, setTimeout은 전역객체가 this
- **생성자 함수 내부** 에서의 this는 새로 만들어질 인스턴스의 자신

## 명시적으로 this를 바인딩하는 방법
- __call__ : call는 첫번째 인자가 this!!

```
let obj = {name:'yoon'}
let say = function(city){
    console.log(`${this.name} {city}`)
}

say('New York') //  New york

```
- __apply__ 