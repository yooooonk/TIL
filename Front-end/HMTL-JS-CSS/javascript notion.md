# Javascript 핵심개념

## 기본형과 참조형의 종류 및 차이점
- 기본형(Primitive Type) : Number, String, Boolean, null, undifined = 값을 그대로 할당
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

## this
- 전역공간에서 : window / global -- 전역객체
- 함수 내부에서 : 기본적으로 window / global -- 전역객체
- 메서드 호출시 : 메소드 호출 주체(메소드명 앞 마지막 foo.bar()) --- this는 obj 객체를 의미, 메서드 내부의 함수(원래는 전역객체)에서 메서드와 같은 this를 사용하려면 메서드 안에서 self = this 등을 선언하고 함수에서 this 대신 self를 사용
``` javascript
var a = 10;
var obj = {
    a : 20,
    b : function(){
        var self = this;
        console.log(this) //20

        function c(){
            console.log(this) //10
            console.log(self.a) // 20
        }
    }
}

obj.b();
```
- callback에서 : 기본적으로 함수 내부에서와 동일,
                    제어권을 가진 함수가 callback의 this를 명시한 경우 그에 따른다
                    개발자가 this를 바인딩한 채로 callback을 넘기면 그에 따른다
``` javascript
var callback = function(){
    console.dir(this);
}

var obj = {
    a : 1,
    b : function(cb){
        cb(this);
    }
}

obj.b(callback)
```            
- 생성자함수에서 : 인스턴스        

## Closure 
- 내부함수가 외부함수의 지역변수에 접근할 수 있고, 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성
- 함수 내부에서 생성한 데이터와 그 유효범위(scope)로 인해 발생하는 특수한 현상/상태
- 함수 최초 선언시의 정보를 유지
- 활용 : 접근 권한 제어, 지역변수 보호, 데이터 보존 및 활용
- 객체 지향 프로그래밍은 외부와의 데이터 연동이 활발하게 이루어져야함

ex] 
``` javascript
function a(){
    var x = 1; 

    function b(){
        console.log(X)
    }
    b();
}
a(); // x
console.log(x); // undefined : 외부에서는 x를 사용할 수 없다
```
ex] 클로저
``` javascript
function a(){
    var x = 1;
    return function b(){
        console.log(X)
    }
}

var c = a();
c(); // x -- 외부에서 사용할 수 있음. 수정은 불가
```

``` javascript
function a(){
    var _x = 1;
    return {
        get x(){return _x;}
        set x(v){_x = v;}
    }
}

var c=a();
c.x = 10; // 외부에서 수정도 가능
```

### Closure로 private member 만들기
1. 함수에서 지역변수 및 내부함수 등을 생성
2. 외부에 노출시키고자 하는 멤버들로 구성된 객체를 return 한다
    - return한 객체에 포함되지 않은 멤버들은 private
    - return한 객체에 포함된 멤버들은 public하다

예) 차량별로 연료량 및 연비는 랜덤, 유저별로 차량 하나씩 고르면 게임시작
각 유저는 자신의 턴에 주사위를 굴려 랜덤하게 나온 숫자만큼 디오함
만약 연료가 부족하면 이동불가
가장 멀리간 사람이 승리
- 수정가능
```javascript
var car = {
    fuel : 10,
    power : 2,
    total : 0,
    run : function(km){
        var wasteFuel = km/this.power;
        if(this.fuel < wasteFuel){
            console.log('이동불가')
            return;
        }
        this.fuel -= wasteFuel;
        this.total += km;
    }
};

car.power = 10;
car.fuel = 1000;

```
- 수정불가능
``` javascript
var createCar = function(f,p){
    var fuel = f;
    var poser = p;
    var total = 0;
    return{ // 외부에 노출할 것만
        run : function(km){
            var wasteFuel = km/power;
            if(fuel < wasteFuel){
                console.log('이동불가')
                return;
            }
        }

    }
}

var car = craeteCar(10,2);
car.run(10) // 이렇게만 사용가능
```

## Prototype
### prototype, constructor, __proto___
- 생성자 prototype ---new---> instance(__proto__생략가능) : 생성자의 rptotype과 인스턴스의 __proto__는 같은 것을 참고
``` javascript
function Person(n,a){
    this.name = n;
    this.age = a;

    var gomu = new Person('고무곰', 30);
    var gomuClone1 = new gomu.__proto__.constructor('고무곰_클론1',10);
    var gomuClone2 = new gomu.constructor('고무곰_클론2',24);

    var gomuProto = Object.getPrototypeOf(gomu);
    var gomuClone3 = new gomuProto.constructor('고무곰_클론3',20);

    var gomuClone3 = new Person.prototype.constructor('고무곰_클론4',15)
}
```

### 메소드 상속 및 동작원리
``` javascript
function Person(n,a){
    this.name = n;
    this.age = a;
}

let gomu = new Person('고무곰',30);
var iu = new Person('아이유', 25);

// 메서드 각각 만듦
gomu.setOlder = function(){
    this.age += 1;
}

iu.setAge = function(){
    this.age += 1;
}

// 한개만 만드는 방법
Person.prototype.getOlder = function(){
    return this.age;
}

Person.__prototype__.age = 10;

iu.getOlder();
gomu.getOloer(); // 30
gomu.__prototype__.getOlder(); //10
```

### Prototype Chaining
- Object prototype 메서드는 자바스크립트의 모든 데이터 타입이 프로토타입 체이닝을 통해 접근할 수 있다
- 객체의 프로토 타입에는 객체 타입에만 사용할 수 있는 프로토타입이 없다.
그래서 Obejct.xx()와 같이 직접 메서드가 많다

### Prototype static 메서드 및 static 프로퍼티
- 클래스.메서드() 생성하면 인스턴스에서는 사용할 수 없다 --- static method
- 클래스.__prototype__.메서드()로 생성해야 인스턴스에서 사용가능

### 클래스 상속 구현
- 예] Person class = getName(), getAge()
      Employee class = getName(), getAge(), getPosition()
      => Employee.prototype = new Person();
         Employee.prototype.constructor = Employee
``` javascript
function Person(name, age){
    this.name = name||'이름없음';
    this.age = age||'나이모름' ;    
}

Person.prototype.getName = function(){
    return this.name;
}

Person.prototype.getAge = function(){
    return this.age;
}

//----- 중복메서드
function Employee(name, age, position){
    this.name = name||'이름없음'; //중복
    this.age = age||'나이모름' ;  // 중복
    this.positoin = position || '직책모름';
}

//------ 상속
Employee.prototype = new Person();
Employee.prototype.constructor = Employee;   // Person에서 getName(), getAge() 상속
Employee.prototype.getPosition = function(){ // getPosition만 만들어면주면됨
    return this.position;
}
```         

---
__reference__
- 인프런 https://www.inflearn.com/course/%ED%95%B5%EC%8B%AC%EA%B0%9C%EB%85%90-javascript-flow