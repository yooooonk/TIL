# 이진 탐색 Binary Search

- 내부 데이터가 이미 정렬 되어 있는 상황에서 사용 가능한 알고리즘
- 탐색 범위를 절반씩 좁혀가며 데이터를 탐색 -> O(logN)의 시간 복잡도

``` java
import java.util.Scanner;

class Hello{
   static int binSearch(int[] a, int n, int key){
        
        int pl = 0; // 검색 범위의 첫 인덱스
        int pr = n-1;   // 검색 범위를 끝 인덱스

        do{
            int pc = (pl+pr)/2;
            if(a[pc]==key){
                return pc;
            }else if(a[pc] < key){
                pl = pc+1;
            }else{
                pr = pc-1;
            }
            
        }while(pl <= pr);

        return -1;
        
   }   

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
                
        System.out.print("요솟수 :");
        int n = stdIn.nextInt();
        System.out.println("오름차순으로 입력하세요");

        
        System.out.print("x[0]:");
        int[] a = new int[n];
        a[0] = stdIn.nextInt(); //while 조건문 때문

        for(int i = 1 ; i<n ; i++){
            do{
                System.out.print("a["+i+"]: ");
                a[i] = stdIn.nextInt();
            }while(a[i]<a[i-1]);            
        }

        System.out.print("검색할 값: ");
        
        int key = stdIn.nextInt();

        int idx = binSearch(a, n, key);
        System.out.println(key+"은(는) a["+idx+"]에 있습니다");
        

    }
}
```


 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- 자료구조와 함께 배우는 알고리즘 입문 JAVA편