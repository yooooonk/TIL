![](https://images.velog.io/images/ouo_yoonk/post/2e202688-7cf5-410c-be55-05393ea1427a/TypeScript__n_-_%EB%B3%80%EC%88%98%EC%99%80_%ED%83%80%EC%9E%85_%EC%A0%95%EC%9D%98%ED%95%98%EA%B8%B0.png)

# 기본타입

-   문자열
-   숫자
-   배열
-   튜플
-   객체
-   boolean
-   null, undefiled
-   | 연산자

```
// 문자열
const str: string = 'hello';

// 숫자
const num: number = 10;

// 배열
const arr: Array<number> = [1, 2, 3];
const heroes: Array<string> = ['Capt', 'tor'];
const items: number[] = [1, 2, 3];

// 튜플
const tuple: [string, number] = ['haha', 1];

// 객체
const obj: object = {};

const person: { name: string; age: number } = {
  name: 'thor',
  age: 1000
};

// boolean
const show: boolean = true;

// undefined, null
let mightBeUndefined : string|undefined = undefined;
let nullableNumber : number|null = null;

// | 연산자
let color:'red'|'orange'|'yellow' = 'red';
color = 'yellow'; //color = 'green'; 
```

# 함수타입

-   함수 타입은 파라미터와 반환값에 타입을 정의한다.
-   return type이 없으면 void 함수
-   `function sum(a: number, b: number):number { return a + b; } sum(10, 20);`
-   파라미터를 제한하는 특성으로 파라미터의 갯수나 타입을 체크한다  
    
    ![](https://images.velog.io/images/ouo_yoonk/post/0546532e-068a-40f5-b40b-af2f493e4b8a/image.png)
    
-   **optional parameter** : 파라미터에`?`를 붙이면 파라미터가 없어도 에러가 나지 않는다.  
    
    ![](https://images.velog.io/images/ouo_yoonk/post/d9c7db7d-4898-43bf-bc17-7a47406206e1/image.png)
    
# 인터페이스
interface는 __클래스__ 또는 __객체__ 를 위한 타입을 지정 할 때 사용하는 문법

- 변수를 정의
- 함수의 인자 정의
- 함수 구조를 정의
- 인덱싱 방식을 정의
- 인터페이스 딕셔너리 패턴
- 인터페이스 확장(상속)

### 변수정의 및 함수의 인자를 정의하는 인터페이스

``` javascript
// 인터페이스 정의
interface User{
    age:number;
    name:string;
}

// 변수 정의
var saram1:User = {
    age:33,
    name:'세호'
}

// 함수의 인자 정의
function getUser(user:User){
    console.log(user);
}

getUser(saram1)

```

### 함수의 스펙(구조)에 인터페이스 활용
``` javascript
interface SumFunction{
    (a:number,b:number):number;
}

let sum: SumFunction;
sum = function(a,b,){
    return a+b
}
```

### 인덱싱 방식을 정의하는 인터페이스
``` javascript
interface StringArray{
    [index:number]:string;
}

const arr:StringArray = ['a','b','c']

// indexing
arr[0] = 'd'
```

### 인터페이스 딕셔너리 패턴
``` javascript
interface StringRegexDictionary{
    [key:string]:RegExp // 정규표현식
}

const obj:StringRegexDictionary = {
    sth:/abc/, // 통과
    sss:'abc', // 에러
}

```

### 인터페이스 확장
``` javascript
interface Person{
    name:string;
    age:number;
}

interface Developer extends Person{    
    language:string;
}

const me:Developer = {
    name:'Gisele',
    age:30,
    language:'javascript'
}
```

# 타입별칭(Type Aliases)
- 타입 별칭은 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미한다.
- `string`,`number`와 같은 간단한 타입 뿐 아니라 `interface` 레벨의 복잡한 타입에도 별칭을 부여할 수 있다.
- 타입 별칭에 제네릭도 사용할 수 있다.
- 타입 별칭은 새로운 타입 값을 생성하는 것이 아니라 정의한 타입에 대해 나중에 쉽게 참고할 수 있게 이름을 부여하는 것과 같다.

``` javascript
type Person = {
    name:string;
    age:number;
}

const seho:Person={
    name:'세호',
    age:30
}
```

### Alias와 Interface의 차이점
||Inferace|Type|
|--|--|--|
|확장	🌷|가능|불가능|
|재할당|가능|불가능|
|목적|구현|데이터를 담기|

좋은 소프트웨어는 확장이 용이해야하기 때문에 `type`보다는 `interface`로 선언해서 사용하는 것을 추천

# 연산자를 이용한 타입정의
## Union Type(|)
하나 이상의 타입을 쓰고 싶을 때, `|` 연산자를 이용해 여러 연산자를 여러 개 연결할 수 있다. (or의 의미)

``` javascript
function logMessage(value:string| number){ // union type
    if(typeof value==='number'){     
        console.log(value.toLocaleString())
    }

    if(typeof value==='string'){
        console.log(value.toLowerCase())
    }

    throw new TypeError('value must be string or number')
}
```
- 타입 추론이 되기 때문에 아래와 같이 해당 타입에 대한 자동완성 기능을 이용할 수 있다.
![](https://images.velog.io/images/ouo_yoonk/post/7f51d9bf-bc31-4c04-bd4a-c2f2b0771e3f/image.png)
![](https://images.velog.io/images/ouo_yoonk/post/b6b341d3-a657-4bec-981a-b51c930e965b/image.png)

- interface 두 개를 합쳤을 때, 공통된 속성에만 접근할 수 있다.
![](https://images.velog.io/images/ouo_yoonk/post/839bd10c-ba45-4b57-afc0-81cca97223c4/image.png)


## Intersection Type(&)
여러 타입을 모두 만족하는 하나의 타이블 의미한다.

![](https://images.velog.io/images/ouo_yoonk/post/66847959-5622-4843-807c-cd7e4a79db21/image.png)

## Union type와 Intersection type의 차이
- union type으로 선언했을 경우, 그 중 하나에 해당하는 타입으로 사용이 가능하지만, intersection type의 경우 모든 항목을 만족하는 타입을 사용해야 한다.
![](https://images.velog.io/images/ouo_yoonk/post/27ea5d68-c24d-46a3-8072-724dd8b6bdff/image.png)



---

**📑 referece**

-   [인프런 - 타입스크립트 입문(캡틴판교)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)
-   [벨로퍼트 - 타입스크립트](https://react.vlpt.us/using-typescript/)
- [Co_ding Note - Type alias와 interface 차이](https://dlgkfka2616.tistory.com/10)