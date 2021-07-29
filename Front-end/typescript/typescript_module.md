# 타입스크립트의 모듈 시스템
타입스크립트 모듈은 전역 변수와 구분되는 자체 유효 범위를 가지며 `export` `import`와 같은 키워드를 사용하지 않으면 다른 파일에서 접근할 수 없다.

``` typescript
// app.ts
import{Todo} from './types'

var item:Todo = {
    title:'할 일 1',
    checked:false
}
```

``` typescript
export interface Todo{
    title:string;
    checked:boolean;
}
```

---
__📑 referece__
-   [인프런 - 타입스크립트 입문(캡틴판교)](https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9E%85%EB%AC%B8?inst=f1ae9299&utm_source=blog&utm_medium=githubio&utm_campaign=captianpangyo&utm_term=banner)