# 삽입정렬 Insertion sort
- 선택한 요소를 그보다 더 앞쪽의 알맞은 위치에 '삽입하는' 작업을 반복하여 정렬하는 알고리즘
- 정렬을 마쳤거나 정렬을 마친 상태에 가까우면 정렬 속도가 매우 빨라짐
- 삽입할 위치가 멀리 떨어져 있으면 이동해야 하는 횟수가 많아짐

```java
class InsertionSort{
    static void insertionSort(int[] a, int n){
        for(int i = 1; i<n; i++){
            int j;
            int tmp = a[i];

            for(j = i; j>0 && a[j-1]>tmp ; j--){
                a[j] = a[j-1];
            }
            a[j] = tmp;
        }
    }

    public static void main(String[] args) {
        int[] a= {40,34,11,65,3,6};

        insertionSort(a, a.length);

        for(int i=0 ; i < a.length ; i++){
            System.out.println(a[i]);
        }

    }
}
```
## 셸 정렬
- 단순 삽입 정렬의 장점은 살리고 단점은 보완한 정렬 알고리즘
- 정렬할 배열의 요소를 그룹으로 나눠 각 그룹 별로 단순 삽입 정렬을 수행하고, 그 그룹을 합치면서 정렬을 반복

```java
class ShellSort{
    static void shellSort(int[] a,int n){
        // 8 1 4 2 7 6 3 5
        for(int h = n/2 ; h>0 ; h/=2){
            System.out.println("h:"+h);
            for(int i = h; i<n ; i++){
                System.out.println("i:"+i);
                int j;
                int tmp = a[i];
                for(j = i-h; j>=0 && a[j]>tmp; j-= h){
                    a[j+h] = a[j];
                    System.out.printf("%3d",j);
                }
                System.out.println();
                a[j+h] = tmp;
            }
        }

    }

    public static void main(String[] args) {
        int[] a= {8, 1, 4, 2, 7, 6, 3, 5};

        shellSort(a, a.length);

       /*  for(int i=0 ; i < a.length ; i++){
            System.out.println(a[i]);
        } */

    }
}
```

---
__reference__
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]