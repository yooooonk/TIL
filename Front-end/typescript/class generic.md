![](https://images.velog.io/images/ouo_yoonk/post/836df572-fd54-4447-9760-4cc44cc4653e/TypeScript__n_-_%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80_%EC%A0%9C%EB%84%A4%EB%A6%AD.png)


# 프로토타입
자바스크립트는 객체를 상속하기 위해 프로토타입이라는 방식을 사용한다. 자바스크립트는 프로토타입 기반언어로서 모든 객체들이 메서드와 속성들을 상속 받기 위한 템플릿으로 프로토타입 객체(prototype object)를 갖는다. 프로토타입 객체로 또 다시 상위 프로토타입 객체로부터 메서드와 속성을 상속 받을 수도 있고 그 상위 프로토 타입 객체로 마찬가지다. 이를 프로토타입 체인이라고 부르고 다른 객체에 정의된 메서드와 속성을 한 객체에서 사용할 수 있도록 한다.

상속되는 속성과 메서드들은 각 객체가 아니라 객체의 생성자의 `prototype`이라는 속성에 정의되어 있다. `prototype` 속성도 하나의 객체이며 프로토타입 체인을 통해 상속하고자 하는 속성과 메서드를 담아주는 버킷으로 주로 사용된다. 

![](https://images.velog.io/images/ouo_yoonk/post/0c70134e-d8ca-4023-86ab-f04b6404f85c/image.png)

객체를 선언했을 때 사용할 수 있는 메서드는 `Object`라는 최상위 프로토타입 객체를 갖고 있기 때문이다.
![](https://images.velog.io/images/ouo_yoonk/post/7a90fef7-864d-432c-b3e4-bf536fecd38e/image.png)


# 클래스
프로토타입 기반의 상속은 유지되고, 문법만 바뀐 것이다. 

``` javascript
class Person{
    // 객체를 만들 때 호출됨
    constructor(name, age){
        this.name = name;
        this.age = age;
        console.log('생성되었음')
    }
}

const inkuk = new Person('사람',30);

```


``` javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}

var capt = new Person('캡틴',100)
```

``` javascript
class Developer{
    // 변수의 접근 범위를 지정할 수 있다.
    private name:string;
    public age:number;
    readonly log:string;

    constructor(name:string,age:number){
        this.name = name;
        this.age = age;
    }
}
```

# 제네릭(Generics)
한가지 타입보다 여러 가지 타입에서 동작하는 컴포넌트를 생성하는데 사용한다. 타입스트립트에서는 타입을 함수의 파라미터처럼 받을 수 있는 것을 제네릭이라고 한다. 함수를 정의할 때가 아닌 _호출하는 시점_ 에 타입을 정의해 파라미터와 반환값에 대한 정확한 타입 추론이 가능하다. 다양한 타입을 받기위해 같은 기능을 하는 함수를 타입만 다르게 여러번 선언할 필요가 없기 때문에 유지보수, 코드 가독성이 좋아진다. 

타입을 정의하지 않으면 any타입
![](https://images.velog.io/images/ouo_yoonk/post/f4114338-b638-4eef-9995-f6cc3c0775fe/image.png)

string 타입을 제네릭으로 넣으면 string 타입으로 바뀜
![](https://images.velog.io/images/ouo_yoonk/post/d8657799-8c22-4881-8c6b-8f23b7660dae/image.png)

## 기존문법과 제네릭의 차이점

- any 타입과 달리 제네릭으로 타입을 정의하면 제네릭 타입에 해당하는 메서드 자동완성 기능을 사용할 수 있다.
- union 타입으로 선언하면 input 값에 대한 에러는 없지만 공통속성에 대한 메서드만 사용할 수 있다.
- 제네릭을 이용해서 타입을 선언하면 자동완성 등 타입선언의 이점을 누릴 수 있다.

## 인터페이스에 제네릭 선언하기
아래의 예제에서 `Email`타입과 `ProductNumber` 타입은 value와 selected 프로퍼티를 갖지만 value의 타입이 달라 두 개의 타입으로 선언했다. 이 경우 interface에 제네릭을 선언해 이용할 수 있다.
``` javascript
interface Email{value:string; selected:boolean}

const emails:Email[] = [
  { value: 'naver.com', selected: true },
  { value: 'gmail.com', selected: false },
  { value: 'hanmail.net', selected: false },
];

interface ProductNumber
{value:number;selected:boolean}

const numberOfProducts:ProductNumber[] = [
  { value: 1, selected: true },
  { value: 2, selected: false },
  { value: 3, selected: false },
];

```
``` javascript
interface Dropdown<T>{
  value:T;
  selected:boolean;
}

const obj:Dropdown<string> = {
  value:'abc',
  selected:false
}
```


---
__📑 referece__
-[MDN - Object prototypes](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes)
-   [인프런 - 타입스크립트 입문(캡틴판교)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)