![](https://images.velog.io/images/ouo_yoonk/post/2e202688-7cf5-410c-be55-05393ea1427a/TypeScript__n_-_%EB%B3%80%EC%88%98%EC%99%80_%ED%83%80%EC%9E%85_%EC%A0%95%EC%9D%98%ED%95%98%EA%B8%B0.png)
# 기본타입
- 문자열
- 숫자
- 배열
- 튜플
- 객체
- boolean
- null, undefiled
- | 연산자

``` javascript
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
- 함수 타입은 파라미터와 반환값에 타입을 정의한다.
- return type이 없으면 void 함수
``` javascript
function sum(a: number, b: number):number {
    return a + b;
  }
  
  sum(10, 20);
```
- 파라미터를 제한하는 특성으로 파라미터의 갯수나 타입을 체크한다
![](https://images.velog.io/images/ouo_yoonk/post/0546532e-068a-40f5-b40b-af2f493e4b8a/image.png)
- __optional parameter__ : 파라미터에`?`를 붙이면 파라미터가 없어도 에러가 나지 않는다.
![](https://images.velog.io/images/ouo_yoonk/post/d9c7db7d-4898-43bf-bc17-7a47406206e1/image.png)