# Greedy 알고리즘(탐욕 알고리즘)

- 최적해를 구하는 상황에서 사용하는 방법
- 여러 경우 중 하나를 선택할 때 그것이 그 상황에서 가장 좋다고 생각하는 것을 선택해 나가는 방식으로 진행해 답을 구한다
- 그 상황에서 가장 좋다고 생각하는 것을 선택해 나가는 바식이기 때문에 가장 좋은 결과를 얻는 것이 보장되는것은 아니다

ex] 돈 바꾸기
``` javascript
<script>

function solution(value){
    
    let changes = [10000,5000,1000,500,100,50,10];
    let counts = [0,0,0,0,0,0,0];

    for(let i = 0; i<changes.length ; i++){
        let cnt = Math.floor(value/changes[i]);

        counts[i] = cnt;

        value = value - (changes[i]*cnt);
    }

    changes.map((item,index)=>{
        console.log(`${item.toLocaleString()}은 ${counts[index]}개`)
    })

}

const value = 32660;


solution(value);
</script>
```