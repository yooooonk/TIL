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


### Arrays.binarySearch에 의한 이진 검색
- 자바는 배열에서 이진 검색을 하는 메서드를 표준 라이브러리로 제공한다
- java.util.Arrays 클래스의 binarySearch 메서드
- 이진 검색 메서드를 직접 코딩할 필요가 없고, 모든 자료형 배열에서 검색할 수 있다
``` java
int idx = AArrays.binarySearch(검색할 array, 검색할 값)
```
``` java
import java.util.Arrays;
import java.util.Scanner;


// 이진 검색으 ㅣ과정을 자세히 출력하는 프로그램
class Hello{
   public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in)   ;

        System.out.print("요솟수 : ");
        int num = stdIn.nextInt();
        int[] x= new int[num];

        System.out.println("오름차순으로 입력하세요");

        System.out.println("x[0]:");
        x[0]=stdIn.nextInt();

        for(int i =1; i<num ; i++){
            do{
                System.out.println("x["+i+"]:");
                x[i] = stdIn.nextInt();
            }while(x[i] < x[i-1]);
        }

        System.out.println("검색할 값: ");
        int ky = stdIn.nextInt();

        int idx = Arrays.binarySearch(x,ky); 

        if(idx<0){
            int insPoint = -idx - 1;
			System.out.println("그 값의 요소가 없습니다.");
			System.out.printf("삽입 포인트는 %d입니다.\n", insPoint);
			System.out.printf("x[%d]의 바로 앞에 %d를 삽입하면 배열의 정렬 상태가 유지됩니다.", insPoint, ky);
        }else{
            System.out.println("x["+idx+"]에 있습니다");
        }       

   }
}
```

### 정렬 되지 않은 배열에서 검색
- 제네릭 메서드를 사용
    - 처리해야 할 대상의 자료형에 의존하지 않는 클래스(인터페이스) 구현방식
``` java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

class PhysExamSearch{
    //신체검사 데이터를 정의
    static class PhyscData{
        private String name;
        private int height;
        private double vision;

        //생성자
        public PhyscData(String name, int height, double vision){
            this.name = name;
            this.height = height;
            this.vision = vision;            
        }

        public String toString(){
            return name+" "+height+" "+vision;
        }
        // 오름차순으로 정렬하기 위한 comparator
        public static final Comparator<PhyscData> HEIGHT_ORDER = new HeightOrderComparator();

        private static class HeightOrderComparator implements Comparator<PhyscData>{
            public int compare(PhyscData d1, PhyscData d2){
                return (d1.height > d2.height)? 1 :
                        (d1.height < d2.height)? -1 : 0;
            }
        }

    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        PhyscData[] x ={
            new PhyscData("서은광", 162, 0.3),
            new PhyscData("이민혁", 172, 0.5),
            new PhyscData("이창섭", 177, 1.0),
            new PhyscData("임현식", 180, 0.2),
            new PhyscData("프니엘", 175, 0.3),
            new PhyscData("정일훈", 182, 0.4),
            new PhyscData("육성재", 184, 1.5)
        };
        
        System.out.println("몇 cm인 사람을 찾고 있나요?:");
        int height=stdIn.nextInt();
        int idx = Arrays.binarySearch(x, new PhyscData("",height, 0.0),PhyscData.HEIGHT_ORDER);

        if(idx<0){
            System.out.println("요소가 없습니다");
        }else{
            System.out.println("x["+idx+"]에 있습니다");
            System.out.println("찾은 데이터 :"+x[idx]);
        }
    }

}
```


 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- 자료구조와 함께 배우는 알고리즘 입문 JAVA편