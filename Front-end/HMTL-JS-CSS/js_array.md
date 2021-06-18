# 자바스크립트 배열 메서드

### 1. 배열 요소를 문자열로
`join(separator?: string): string;`

``` javascript
    const fruits = ['a','b','c'];
    const jj =  fruit.join('')

    console.log(jj) // 'abc'
```

### 2. 문자열을 배열로
`split(separaotr?:string):T[]`
``` javascript
    const fruits = ['a','b','c'];
    const jj =  fruit.join('')

    console.log(jj) // 'abc'
```

### 3. 배열 요소를 거꾸로
`reverse():T[]`
- 원본 배열도 바뀜
``` javascript
    const arr = ['a','b','c'];
    const result =  arr.reverse()

    console.log(result) // ['c','b','a']
	console.log(arr) // ['c','b','a']
```

### 4. 배열 자르기
`splice(start: number, deleteCount?: number): T[]`
 
- start index부터 deleteCount(개수)만큼 자름
- 잘린 요소 리턴
- 원본 배열도 바뀜
``` javascript
    const arr = ['a','b','c','d','e'];    
    const result =  arr.splice(0,2)
    console.log(result) // ['a','b']
	console.log(arr) // ['c','e','e']
    
    const arr2 = ['a','b','c','d','e'];    
    const result2 = arr.splice(0,2,['aa'])
    console.log(result) // ['a','b']
	console.log(arr) // ['aa','c','e','e']

    
```

### 5. 배열 자르기2
`slice(start?: number, end?: number): T[]`
- end idx 앞에까지 자름
- 자른! 배열 리턴
- 원본 배열 변하지 않음
``` javascript
    const arr = ['a','b','c','d','e'];
    const result =  arr.slice(2,5)

    console.log(result) // ['c','d','e']
	console.log(arr) // ['a','b','c','d','e']
```

### 6. 조건을 만족하는 첫 번째 인자찾기
`find(value: T, index: number, array: T[]) => unknown, thisArg?: any): number | undefined`
- 첫 번째 인자인 콜백함수에 만족하는 첫 번째 index 리턴
- 콜백함수는 boolean을 return 해야함
```javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    
    const result = students.find((student)=>{
    	return student.score === 100
    })
    
    console.log(result)//1
```

### 7. 조건을 만족하는 모든 인자 찾기 
`filter(predicate: (value: T, index: number, array: T[]) => unknown, thisArg?: any): T[]`

- 첫 번째 인자인 콜백함수에 만족하는 첫 번째 index 리턴
- 콜백함수는 boolean을 return 해야함
``` javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    
    const result = students.filter((student)=>{
    	return student.score >= 95
    })
    
    console.log(result)// [{name:'이민혁',score:'100'},{name:'육성재',score:95}]
```

### 8. 배열 요소를 조작해 새로운 값으로 변환  
`Map(callbackfn: (value: T, index: number, array: T[]) => U, thisArg?: any): U[]`

``` javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    
    const result = students.map((student)=>{
    	return student.score 
    })
    
    console.log(result)// [81,100,30,80,90,95]
```
  
### 9. 조건을 만족하는 요소가 있는지 없는지 
`some(predicate: (value: T, index: number, array: T[]) => unknown, thisArg?: any): boolean`

``` javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    
    const result = students.some((student)=>{
    	student.score < 50
    })
    
    console.log(result)// true
```

### 10. 모든 요소가 조건을 충족하는지 
`every(predicate: (value: T, index: number, array: T[]) => unknown, thisArg?: any): boolean`

 ``` javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    
    const result = students.some((student)=>{
    	student.score > 50
    })
    
    console.log(result)// false
```

### 11. 배열의 모든 요소를 누적 
`reduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T, initialValue: T): T`

- acc : return으로 누적된 값
- curr : 배열의 아이템
``` javascript
	const students = [
    	{name:'서은광',score:81},
        {name:'이민혁',score:100},
        {name:'이창섭',score:30},
        {name:'임현식',score:80},
        {name:'프니엘',score:90},
        {name:'육성재',score:95}        
    ]
    // 평균 구하기
    const result = students.reduce((acc,curr)=>{
    	return acc+curr.score
    },0) // initail value 0
    
    console.log(result)// 476
    console.log(result/students.length)
 ```

### 12. 정렬
`sort(compareFn?: (a: T, b: T) => number): this`

``` javascript
	// 오름차순	
	const arr = [1,2,3,4]
    const result = arr.sort((a,b)=> a-b)
    
    // 내림차순
    const arr2 = [1,2,3,4]
    const result = arr2.sort((a,b)=> b-a)
    
    
```