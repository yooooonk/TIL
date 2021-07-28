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

### Typescript Language Server