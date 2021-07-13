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
interface는 클래스 또는 객체를 위한 타입을 지정 할 대 사용하는 문법
- 함수의 인자 정의
- 함수 구조를 정의
- 인덱싱 방식을 정의
- 인터페이스 딕셔너리 패턴
- 인터페이스 확장(상속)

### 함수의 인자를 정의하는 인터페이스
``` javascript
interface User{
    age:number;
    name:string;
}

var saram1:User = {
    age:33,
    name:'세호'
}

function getUser(user:User){
    console.log(user);
}

getUser(saram1)


```

---

**📑 referece**

-   [인프런 - 타입스크립트 입문(캡틴판교)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)
-   [벨로퍼트 - 타입스크립트](https://react.vlpt.us/using-typescript/)