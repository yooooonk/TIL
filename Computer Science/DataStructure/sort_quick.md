# 퀵 정렬(Quick sort)
- 퀵 정렬이란 피벗을 기준으로 큰 값과 작은 값을 서로 교체하는 정렬기법
- 일반적으로 사용되고 있는 아주 빠른 정렬 알고리즘
- 값을 서로 교체하는 데 N번, 엇갈린 경우 교체 이후에 원소가 반으로 나누어지므로 전체 원소를 나누는데 평균적으로 logN번이 소요되므로 평균적으로 O(NlogN)의 시간 복잡도를 가진다
- 원소를 절반식 나눌 때 logN의 시간 복잡도가 나오는 대표적인 예시는 완전 이진트리이다.
완전 이진트리 형태는 흔히 컴퓨터 공학에서 가장 선호하는 이상적인 형태이다

  

### 퀵 정렬 구현
``` java
class QuickSort{
    static void swap(int[] a, int idx1, int idx2){
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;
    }

    static void quickSort(int[] a,int left, int right){
       int pl = left;
       int pr = rigth;
       int x = a[(pl+pr)/2];

       do{
           while(a[pl] < x) pl++;
           while(a[pr] > x) pr--;
           if(pl<=pr){
               swap(a,pl++,pr--);
           }
       }while(pl<=pr);

       if(left<pr) quickSort(a,left,pr);
       if(pl<right) quickSort(a, pl,right);
    }

    public static void main(String[] args) {
        int[] a= {8, 1, 4, 2, 7, 6, 3, 5};

        quickSort(a, 0, a.length-1);

       /*  for(int i=0 ; i < a.length ; i++){
            System.out.println(a[i]);
        } */

    }
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]