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

---
__📑 referece__
-[MDN - Object prototypes](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes)