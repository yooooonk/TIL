# 병합정렬 Merge Sort
- 분할 정복 방식
- 절반씩 합치면서 정렬하면, 전체 리스트가 정렬
- 병합할 때는 리스트의 맨 앞 원소부터 차례대로 채워넣는다
- 시간 복잡도 : O(NlogN)
- 퀵소트와 같은 시간 복잡도를 갖지만 실행시에 별도의 저장공간이 필요하므로 공간복잡도가 높음

``` javascript
function mergeSort(array){
    console.log('mergeSort',array)
    if(array.length < 2){
        return array
    }

    const mid = Math.floor(array.length/2)
    
    const left = array.slice(0,mid)
    const right = array.slice(mid)

    return merge(mergeSort(left),mergeSort(right));

    function merge(left, right){
        console.log('merge',left,right)
        const resultArray = []
        let leftIndex = 0;
        let rightIndex = 0;

        while(leftIndex < left.length && rightIndex<right.length){
            if(left[leftIndex] < right[rightIndex]){
                resultArray.push(left[leftIndex])
                leftIndex++
            }else{
                resultArray.push(right[rightIndex]);
                rightIndex++
            }
        }

        return resultArray.concat(left.slice(leftIndex),right.slice(rightIndex))
    }
}

console.log(mergeSort([5,4,3,2,1]))

```

---
__reference__
- https://www.youtube.com/watch?v=QAyl79dCO_k
- https://im-developer.tistory.com/134
- fastcampus [알고리즘 - 나동빈]