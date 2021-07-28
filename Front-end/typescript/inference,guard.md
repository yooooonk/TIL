# 타입추론

타입스크립트가 코드를 해석해 나가는 동작을 의미한다.

### 인터페이스와 제네릭을 이용한 타입 추론 방식
![](https://images.velog.io/images/ouo_yoonk/post/3a824772-d3b0-465e-ab17-3e915a16ab57/image.png)
제네릭을 선언했을 때, 타입스크립트가 제네릭을 이용해 타입을 추론해 변수에 필요한 속성을 보장해준다. 

### 복잡한 구조에서의 타입 추론 방식
![](https://images.velog.io/images/ouo_yoonk/post/3d9c6541-ea61-4d42-964a-17c6adeff868/image.png)

DetailedDropdown에서 value와 tag가 제네릭 타입으로 정의해야 한다.

### Best Common Type 추론 방식
![](https://images.velog.io/images/ouo_yoonk/post/b405a31a-2c5e-4733-ad1c-6ebdfa935e4f/image.png)

Best Common Type은 타입스크립트가 타입을 해석하는 알고리즘
모든 타입을 union으로 묶어감

# 타입단언
Typescript의 타입 추론 기능은 매우 강력하지만 어쩔 수 없는 한계가 존재한다. 타입 단언은 타입스크립트 컴파일러가 실제 런타임에 존대할 변수의 타입과 다르게 추론하거나 너무 보수적으로 추론하는 경우에 `프로그래머가 수동으로 컴파일러한테 특정 변수 타입에 대해 힌트를 주는 것`이다. `as` 키워드를 사용한다.

타입 캐스팅과의 차이는 타입 캐스팅은 컴파일타임과 런타임에서 모두 타입을 변경시키지만 타입 단언은 오직 컴파일타임에서만 타입을 변화시킨다는 것이다.

아래의 예시에서 b=aa라고 했을 때 b를 any로 추론한다.
``` javascript
var aa;
aa = 20; // number로 할당
aa = 'a' // string으로 재할당
```
![](https://images.velog.io/images/ouo_yoonk/post/8466dee4-ad46-4076-b891-85fde30cdc50/image.png)

하지만 aa에 최종적으로 string을 할당했기 때문에 aa의 타입은 string이므로, as로 string 타입임을 단언하면 b를 string으로 추론을 하게된다.
![](https://images.velog.io/images/ouo_yoonk/post/72a26af4-7355-41b5-8773-1b84d6d64431/image.png)


ex] DOM API 조작에서 타입단언의 예
``` html
<div id="app">hi</div>
```
![](https://images.velog.io/images/ouo_yoonk/post/9ed0253a-794f-4195-a133-4558a22147c6/image.png)

DOM API의 타입도 일반적으로 제공을 하지만 실제로는 DOM API를 사용하는 시점에 해당 element가 있다는 것을 보장하지 않는다. 사실상 `null와 HTMLDivElement` 타입을 갖게 되는 것이다. 
따라서 아래와 같은 패턴으로 사용한다.
``` javascript
var div = document.querySelector('div') 


if(div){
  div.innerText;
}
```

타입 단언을 해주면 null 타입을 갖지 않게 되므로 아래와 같이 사용할 수 있다.
``` javascript
var div = document.querySelector('div') as HTMLDivElement;
div.innerHtext;
```

# 타입가드
타입가드는 타입 단언을 좀 더 깔끔하게 할 수 있도록 도와준다. 타입 가드는 런타임에서의 타입 체크를 컴파일러에게 알려주는 기능이다. `is`키워드를 사용한다.

``` javascript
interface Developerr{
    name:string;
    skill:string;
}

interface Personn{
    name:string;
    age:number;
}

function introduce() : Developerr|Personn { 
    return {name:'Tony', age:33, skill:'Iron Making'}
}
```

![](https://images.velog.io/images/ouo_yoonk/post/c00b618a-60e1-4e33-b7dd-1f5a670ef90e/image.png)

공통속성아 아닌 타입을 사용하기 위해서 타입단언을 이용해 아래와 같이 사용하면 가독성이 떨어진다.

``` javascript
if((tonytony as Developerr).skill){
    var skill = (tonytony as Developerr)
    console.log(skill)
}else if ((tony as Person).age){
    var age = (tonytony as Personn)
    console.log(age)
}
```

`isDeveloper`라는 타입가드를 정의하면 같은 로직을 아래와 같이 사용할 수 있다.

``` javascript
// 타입가드를 정의
function isDeveloper(target:Developerr|Personn):target is Developerr {
    return (target as Developerr).skill !== undefined;
}

if(isDeveloper(tonytony)){
    console.log(tonytony.skill)
}else{
    console.log(tony.age)
}

```

---
__📑 referece__
- [타입단언](https://hyunseob.github.io/2017/12/12/typescript-type-inteference-and-type-assertion/)