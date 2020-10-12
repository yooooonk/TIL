# 버블정렬
- 이웃한 두 요소의 대소 관계를 비교해 교환을 반복
- 시간복잡도 : O(N²)

```java
class BubbleSort{
    
    static void swap(int[] a, int idx1, int idx2){
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    static void bubbleSort(int[] a, int n){
        int k = 0;
        while(k<n-1){
            int last = n-1;
            
            for(int j = n-1; j>k ; j--){
                if(a[j-1]>a[j]){
                    swap(a, j-1, j);
                    last = j;  
                }
            }
            k=last;
        }
        
    }

    public static void main(String[] args) {
        int a[] = {6,4,3,7,1,9,8};

        bubbleSort(a, a.length);                
    }
}
```



---
__reference__
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]