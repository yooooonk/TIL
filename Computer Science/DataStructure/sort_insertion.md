# 삽입정렬 Insertion sort
- 선택한 요소를 그보다 더 앞쪽의 알맞은 위치에 '삽입하는' 작업을 반복하여 정렬하는 알고리즘

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
### 이진삽입정렬
```java
```

---
__reference__
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]