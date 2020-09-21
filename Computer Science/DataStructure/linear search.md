## 순차 탐색
- 특정한 원소를 찾기 위해 원소를 순차적으로 하나씩 탐색하는 방법
- 데이터 정렬 유무에 상관없이 가장 앞에 있는 원소부터 하나씩 확인해야 한다는 점에서 O(N)의 시간 복잡도
- 배열은 검색은 빠르지만 데이터를 추가하기 위한 비용이 많이 든다
- 데이터 집합이 있을 때 검색만 한다면 계산 시간이 짧은 것을 선택하면 됨. 그러나 데이터 집합에 대한 검색뿐 아니라 데이터의 추가, 삭제 등을 자주하는 경우라면 검색 이외의 작업에 소요되는 비용을 종합적으로 평가하여 알고리즘을 선택해야 한다.
예를 들어 데이터 추가를 자주하는 경우에 검색이 빠르더라도 데이터의 추가 비용이 많이 들어가는 알고리즘은 피해야 한다

``` java
import java.util.Scanner;

class Hello{
   static int linearSearch(int[] x, int num, int key){
      /* while(true){
            if(i == num){
                return -1;
            }
            if(x[i] == key){
                return i;
            }
            i++;
        } */
        for(int  i = 0 ; i<num; i++){
            if(x[i] == key){
                return i;
            }
        }
        return -1;
   }   

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        
        System.out.print("요솟수 :");
        int num = stdIn.nextInt();

        int[] x = new int[num];

        for(int i = 0;i<num; i++){
            System.out.print("x["+i+"] :");
            x[i] = stdIn.nextInt();
        }

        System.out.print("검색할 값: ");
        int key = stdIn.nextInt();

        int idx = linearSearch(x, num, key);
        if(idx == -1){
            System.out.println("찾는 값이 없어요");
        }else{
            System.out.println("검색할 값"+key+"는 x["+idx+"]에 있습니다");
        }
    }
}
```

### 보초법
- 선형 검색은 반복하 때 마다 두 가지의 종료 조건(검색할 값을 발견한 경우, 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우)을 모두 판단하는데, 종료 조건을 검사하는 비용도 줄이는게 좋다
- 이 비용을 반으로 줄이는 방법을 보초법(sentinel method)라고 함
- __검색하기 전에 검색하고자 하는 키 값을 맨 끝 요소에 저장__ 이때 저장하는 값을 보초(sentinel)이라고 함
``` java
import java.util.Scanner;

class Hello{
   static int linearSearch(int[] x, int num, int key){
        
        int i = 0;
        while(true){
            if(x[i] == key){
                break;
            }
            i++;
        }

        return i == num? -1 : 1;
   }   

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        
        System.out.print("요솟수 :");
        int num = stdIn.nextInt();

        int[] x = new int[num+1]; // 빈 값을 하나 넣음

        for(int i = 0;i<num; i++){
            System.out.print("x["+i+"] :");
            x[i] = stdIn.nextInt();
        }

        System.out.print("검색할 값: ");
        int key = stdIn.nextInt();

        int idx = linearSearch(x, num, key);
        if(idx == -1){
            System.out.println("찾는 값이 없어요");
        }else{
            System.out.println("검색할 값"+key+"는 x["+idx+"]에 있습니다");
        }
        

    }
}
```

---
__REFERENCE__
- 자료구조와 함께 배우는 알고리즘 입문 JAVA편