# 배열 Array

- 배열은 같은 형의 구성 요소가 직선 모양으로 연속하여 줄지어 있는 단순한 자료구조
- 배열 안의 모든 구성 요소의 형은 같고 직선 모양으로 줄지어 있다
- 배열 초기화를 사용하면 배열 본체의 생성과 동시에 각 요소의 초기화가 가능하다
``` java
class IntArrayInit{
     public static void main(String[] args) {
        // 배열선언방법 1
        int[] a= {1,2,3,4,5};

        // 배열선언방법2
        int[] b = new int[] {1,2,3,4,5};

        // 배열복제
        int[] c = a.clone();
    }
}
```

### 배열 요소의 최댓값 구하기
```java
class Max{
  
     static void maxOf(int[] a){
         int max = a[0];
         final int cnt = a.length;
         
         System.out.println("키의 최댓값을 구합니다"); 
         System.out.println("사람수 : "+cnt);
        
         for(int i = 0 ; i< cnt ; i++){
             System.out.println("a["+i+"]:"+a[i]);            
            if(a[i] > max) max = a[i];
         }
         System.out.println("최댓값은 "+max+"입니다");
     }

    public static void main(final String[] args) {
        int array[] = new int[] { 1, 2, 3, 4, 5 };
        maxOf(array) ;
    }
}
```

### 배열 요소를 역순으로 정렬하기
= 교환
``` java
class Reverse{

    static void swap(int[] a, int idx1, int idx2){
        int t = a[idx1];
        a[idx1] = a[idx2];
        a[idx2] = t;

    }
  
     static void reverse(int[] a){
         for(int i =0;i<a.length;i++){
             swap(a,i,a.length-i-1);
         }
     }

    public static void main(final String[] args) {
        
        //Scanner stdIn = new Scanner(System.in);

        System.out.println("요솟수 : ");
        int num = stdIn.nextInt();

        int[] x = new int[num];

        for(int i = 0;i<num;i++){
            
            System.out.println("x["+i+"]:");
            x[i] = stdIn.nextInt();
        }

        reverse(x);

        System.out.println("요소를 역순으로 정렬했습니다");
        for(int i =0;i<num;i++){
            System.out.println("x["+i+"]="+x[i]);
        }

    }
}
```

### 두 배열의 비교
``` java
class ArrayEqual{

    static boolean equals(int[] a, int[] b){
        if(a.length != b.length) return false;

        for(int i = 0; i<a.length ; i++){
            if(a[i] != b[i]) return false;
        }

        return true;
    }

    public static void main(String[] args) {
        int[] a = {1,2,3,4,5};
        
        System.out.println("a[]의 요수 : "+ a.length);

        int[] b = {1,2,3,4,5};

        System.out.println("b[]의 요수 : "+ b.length);

        System.out.print("배열 a와 b는");
        System.out.println(equals(a, b)?"같다":"같지않다");

    }    
}
```

### 기수 변환
``` java
class Hello{

    static int cardConvR(int a, int r, char[] d){
        int digits = 0;
        String dchar = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        do{
            d[digits++] = dchar.charAt(x%r); // 나머지를 저장
            x /= r;
        }while(x != 0);
        return digits;
    }
    
}
```

### 소수의 나열
``` java
class Hello{

    static void primeNumber1(){
        int counter = 0;

        for(int n = 2;n<=1000;n++){
            int i;
            for(i = 2;i<n;i++){
                counter++;
                if(n%i==0) break;                
            }
            if(n==i){
                System.out.println(n);
            }
            
        }
        System.out.println("나눗셈을 수행한 횟수:"+counter);
    }

    static void primeNumber2(){
        int counter = 0;
        int ptr = 0;
        int[] prime = new int[500];

        prime[ptr++] = 2;

        for(int n = 3 ; n <= 1000; n+=2){ // 홀수만, 짝수는 다 2로 나눠짐
            int i;
            for(i=1;i<ptr;i++){
                counter ++;
                if(n%prime[i] == 0) break;
            }
            
            if(ptr == i) prime[ptr++] = n;
        }

        for(int i = 0 ; i <ptr ; i++){
            System.out.print(prime[i]+" ");;
        }
        System.out.println("나눗셈을 수행한 횟수:"+counter);
    }

    static void primeNumber3(){
        int counter = 0;
        int ptr = 0;
        int[] prime = new int[500];

        prime[ptr++] = 2;
        prime[ptr++] = 3;

        for(int n = 5; n<=1000;n+=2){
            boolean flag = false;
            for(int i = 1 ; prime[i]*prime[i]<=n ; i++){
                counter += 2;

                if(n%prime[i] == 0){
                    flag = true;
                    break;
                }
            }

            if(!flag){
                prime[ptr++] = n;
                counter++;
            }
        }
        for(int i = 0; i<ptr; i++){
            System.out.println(prime[i]);
        }
        System.out.println("곱셈과 나눗셈을 수행한 횟수: "+counter);

    }

    public static void main(String[] args) {
        
        //primeNumber1();
        primeNumber3();
    }
}
```

### 다차원 배열
``` java
int[][] x = new int[2][4];
```
ex] 한 해의 경과 일 수 
``` java
import java.util.Scanner;

class Hello{

    static int[][] mdays = {
        {31,28,31,30,31,30,31,31,30,31,30,31}, //평년
        {31,29,31,30,31,30,30,31,31,30,31,30,31} //윤년
    };

    // 윤년 : 1, 평년 : 0
    static int isLeap(int year){
        return (year % 4 == 0 && year % 100 != 0 || year % 400 == 0)? 1: 0;
    }

    static int dayOfYear(int y, int m, int d){
        int days = d;

        for(int i = 1; i<m;i++){
            days += mdays[isLeap(y)][i-1];            
        }
            
        return days;
    }

    public static void main(String[] args) {
        Scanner stdIn = new Scanner(System.in);
        int retry;

        System.out.println("그 해 경과 일수를 구합니다");

        do{
            System.out.print("년:"); int year = stdIn.nextInt();
            System.out.print("월:"); int month = stdIn.nextInt();
            System.out.print("일:"); int day = stdIn.nextInt();

            System.out.printf("그 해 %d일째입니다\n",dayOfYear(year, month, day));

            System.out.print("한 번 더 할까요? (1.예 / 0.아니오) :");
            retry = stdIn.nextInt();
        }while(retry == 1);
    }
}
```

# 클래스
- 임의의 데이터형을 자유로이 조합하여 만들 수 있는 자료구조
### 클래스의 종류
- 공개 클래스 : public. 다른 패키지에서 사용할 수 있는 공개 클래스
- final 클래스 : 새로운 클래스를 상속할 수 없다
- 파생 클래스 : B extends A라면 B가 A의 서브 클래스


---
reference
- 자료구조와 함께 배우는 알고리즘 입문 JAVA편