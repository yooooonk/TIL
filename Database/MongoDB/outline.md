# mongoDB
- Document-Oriented(문서 지향적) NoSQL데이터베이스
- NoSQL : RDBMS의 한계를 극복하기 위한 새로운 형태의 데이터베이스
- {key:value} < Documents < Collections < Database
     - Documents : RDMS의 recode와 유사한 개념으로 JSON object 형태의 key-value 쌍으로 이루어진 데이터구조로 구성, value에 다른 document, array, document array가 포함될 수 있다
     ``` javascript
     {
        _id: ObjectId("5099803df3f4948bd2f98391"),
        name: { first: "Alan", last: "Turing" },
        birth: new Date('Jun 23, 1912'),
        death: new Date('Jun 07, 1954'),
        contribs: [ "Turing machine", "Turing test", "Turingery" ],
        views : NumberLong(1250000)
     }
     ```
    - Collection : RDMS의 table과 유사한 개념, Document들의 집합
    - Database : Collections들의 물리적인 컨테이너

## Mongoose
- 몽고 DB 사용을 위한 다양한 기능을 추가하고 몽고 DB를 더 편리하게 이용하기 위해 사용하는 모듈
- 몽구스를 이용해 데이터를 만들고 관리하기 위해 먼저 Schema를 만들고 그 스키마로 모델을 만든다
- mongoDB를 사용할 때 필수는 아님
- 몽구스가 model class(collection)와 model instance(documents)를 제공해줌
---
__reference__
- https://poiemaweb.com/mongdb-basics
