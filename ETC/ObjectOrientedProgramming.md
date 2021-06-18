![](<https://images.velog.io/images/ouo_yoonk/post/f8bb8c25-4900-4c33-9826-9d0a304fdb6a/OOP(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D).png>)

# 객체 지향 프로그래밍이란?

> 필요한 데이터를 추상화시켜
> 상태와 행위를 가진 객체를 만들고
> 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법

## 장점과 단점

- 코드 재사용성 유리
- 유지보수가 쉽다
- 대형 프로젝트에 적합하다

- 초기 설계가 중요하다
- 처리속도가 상대적으로 느리다
- 객체가 많으면 용량이 커질 수 있다.

## 특징

### 클래스와 인스턴스(객체)

- class : 같은 특징들끼리 묶은 template. 어떤 문제를 해결하기 위한 데이터를 만들기 위해 추상화를 거쳐 집단에 속하는 속성과 행위를 변수와 메서드로 정의한 것
- 인스턴스(객체) : 클래스에서 정의한 것을 토대로 실제 메모리상에 할당된 것으로 실제 프로그램에서 사용되는 데이터

### 추상화

- 자료의 공통의 속성이나 기능을 묶어 이름을 붙인 것
- 클래스를 정의하는 것

### 캡슐화

- 추상화해서 뽑은 속성과 행위를 관련있는 것끼리 묶는 것
- 외부에서 접근이 필요한 부분을 제외하고 내부로 숨긴다
- 내부 응집도는 높을수록, 외부 결합도는 낮을수록 좋다
- getter와 setter : 멤버 변수는 private으로 선언해 외부에서 직접 접근하지 못하게 하고, 메서드를 통해서 접근하게 한다. 올바르지 않은 입력에 대해 처리할 수 있게 됨

### 상속

- 부모클래스의 속성과 기능을 그대로 이어받아 사용할 수 있게하고, 기능의 일부분을 변경할 수 있다.

### 다형성

- 하나의 변수, 함수가 상황에 따라 다른 의미로 해석될 수 있는 것
- 오버라이딩 : 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용
- 오버로딩 : 같은 이름의 메서드 여러개를 가지면서 매개변수의 유형과 개수가 다르게 하는 것
- 코드의 가독성이 높아지고, 일관성이 생긴다.

## 설계원칙 - SOLID

### SRP - 단일 책임의 원칙

- Single Responsibility Principle
- 한 클래스에 단 하나의 책임만 수행하도록 해 변경 사유가 될 수 있는 것을 하나로 만들어야 한다.
- 책임 : 해야하는 것, 할 수 있는 것, 해야하는 것을 잘 할 수 있는 것

### OCP - 개방/폐쇄의 원칙

- Open Closed Principle
- 확장에는 열려있고, 변경에는 닫혀있어야 한다.
- 기존의 코드를 변경하지 않으면서 기능을 추가할 수 있도록 설계되어야 한다.

### LSP - 리스코프 치환 원칙

- Liskov Substituetion Principle
- B가 A의 자식 타입이면 부모 타입인 A 객체는 자식 타입인 B로 치환해도, 작동에 문제가 없어야 한다

### ISP - 인터페이스 분리 원칙

- Interface Segregation Principle
- 인터페이스를 클라이언트에 특화되도록 분리시킨다.
- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.

### DIP - 의존 역전 원칙

- Dependency Inversion Principle
- 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것보다는 변화하기 어려운 것, 거의 변화가 없는 것에 의존하라.

# 자바스크립트의 Class와 객체

- ES6 이전에는 클래스를 만들지 않고 object를 만들었다. proto-type을 기반으로 문법상으로 class를 구현했다.

```javascript
class Person {
  contructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```

1. 객체 선언 방법

- object literal

```javascript
const obj = { key: value };
```

- object constructor syntax

```javascript
const obj = new Person('kim', 30);
```

2. 객체 접근방법

```javascript
console.log(obj.name); // kim

console.log(obj['name']); //kim
// key를 정확히 모를 때,  동적으로 사용 가능
```

3. constructor function

- 순수하게 object를 만드는 함수
- 첫 글자를 대문자로

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}
```

4. In operator

- 객체 안에 key가 있는지 확인

```javascript
console.log('name' in obj); //true
```

5. for in과 for of

```javascript
	for k in obj :
    	console.log(k) // name, age

	for v of obj :
		console.log(v) // kim, 30
```

6. cloning

- object는 참조형 자료형이므로 shallow copy

```javascript
const obj2 = obj;
obj2.name = 'Lee';
console.log(obj.name); // Lee
```

- deep copy : Object.assign()

```javascript
const obj3 = Object.assign({}, obj);
obj3.name = 'Park';
console.log(obj.name); // Lee
```

---

**&#128209; reference**

- [드림코딩 by 앨리](https://www.youtube.com/watch?v=_DLhUBWsRtw&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=6)
- https://jeong-pro.tistory.com/95
- https://gmlwjd9405.github.io/2018/07/05/oop-solid.html
