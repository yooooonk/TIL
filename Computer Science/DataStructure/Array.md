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