# 정렬 알고리즘

## 선택정렬 O(N²)
- 가장 작은 요소부터 선택해 알맞은 위치로 옮겨서 순서대로 정렬하는 알고리즘
```javascript
let a = [1,3,5,67,7];
let sort = [];
while(a.legnth != 0){
    sort.push(Math.min.apply(null,a));

    a.splice(a.indexOf(Math.min.apply(null,a)),1);
}
```

## 삽입정렬 O(N²)
- 순서대로 선택한 요소를 알맞은 위치에 '삽입하는' 작업을 반복해 정렬
```javascript
let array = [10,3,4,66,23,12,11];
let sort = [];
let n = array.length;

function indexOfInsertion(sort, inst){
    for(var i in sort){
        if(inst <sort[i]){
            return i;
        }
    }

    return sort.length;
}

for(var i = 0; i<n;i++){
    inst = array.shift();
    idx = indexOfInsertion(sort,inst);
    sort.splice(idx,0,inst);
}
```

## 병합정렬 O(NlogN)
- 배열을 앞부분과 뒷부분으로 나누어 각각 정렬한 다음 병합하는 작업을 반복
```javascript
let array = [10,3,4,66,23,12,11];

function mergeSort(array){
    let n = array.length;
    let result = [];

    if(n<=1){
        return array;
    }
    let cnt  =0;
    let mid = parseInt(n/2);
    let g1 = mergeSort(array.slice(0,mid));
    let g2 = mergeSort(array.slice(mid,));

    while(g1.length!=0 && g2.length!=0){
        if(g1[0]<g2[0]){
            result.push(g1.shift())
        }else{
            result.push(g2.shift());
        }
        console.log(cnt++,result);
    }

    while(g1.length!=0 ){
        result.push(g1.shift())        
    }

    while(g2.length!=0 ){
        result.push(g2.shift())        
    }
    return result;
}

console.log(mergeSort(array))
```

## 퀵정렬
- 기준점을 잡아서 앞부분, 뒷부분으로 나누어서 정렬하고 병합
```javascript
let array = [66,77,54,32,10,5,11,13];

function quick(array){
    let n = array.length;
    
    if(n <= 1){
        return array;
    }

    let pivot = [array.shift()];
    console.log(pivot)
    let g1 = [];
    let g2 = [];

    for(let i in array){
        if(array[i] < pivot){
            g1.push(array[i]);
        }else{
            g2.push(array[i]);
        }
    }

    return quick(g1).concat(pivot,quick(g2))
}

console.log(quick(array))
```

---
__reference__
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]