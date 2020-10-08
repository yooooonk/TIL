# 재귀함수

### 1부터 100까지 합과 곱
- for문 이용 : O(n)
- 가우스 법 이용 : O(1)
``` javascript
            // 반복문을 이용한 1부터 100까지의 합과 곱
            // O(n)
            let s = 0;
            let n = 100;
            for(var i=1 ; i<= n; i++  ){
                s+=i;
            }

            console.log(s)

            // 가우스의 덧셈
            // O(1)
            let g = 0;
            g = n*(n+1)/2;
            console.log(g)

            function fs(n){
                if(n<=1){
                    return 1;
                }

                return n+f(n-1)
            }

            function fm(n){
                if(n<=1){
                    return 1;
                }

                return n*fm(1);
            }

            console.log(`재귀함수 ${fs(100)}`)
```

### 이진수 변환
``` javascript
  let x = 11;
           let result = '';

           while(true){
               if(x%2==0){
                   result += '0'
               }else{
                   result += '1'
               }

               x = Math.floor(x/2);
               if(x==1 || x==0){
                   result += String(x);
                   break;
               }
           }

           console.log(result.split('').reverse().join(''))

           function binary(n){
               if(n ==1 || n==0){
                   return String(n)
               }

               return binary(Math.floor(n/2)) + String(n%2)
           }

           console.log(binary(11))
```

### 문자열 뒤집기
``` javascript
const x = 'abcdefg';
           let n = x.length -1;

           function reverse(x){
               if(n==0){
                   return x.charAt(n);
               }
               
               return x.charAt(n--)+reverse(x);
           }

           console.log(reverse(x))
```

### 각 자릿수의 합
``` javascript
function rec(x){
    if(x.length == 1){
        return parseInt(x,10);
    } 
            
    return parseInt(x[x.length-1],10) + rec(x.slice(0,x.length-1))
}

console.log('재귀',rec('123123'))
```

### 팩토리얼
```javascript
function f(n){
              if(n<=0){
                  return 1
              }else{
                  return n*f(n-1);
              } 
          }

          console.log(f(3))
```

### 유클리드 호제법
- 두 정수의 최대공약수를 재귀적으로 구하는 방법
- 두 정수가 주어졌을 때 큰 값을 작은 값으로 나누었을 때 나누어떨어지는 가장 작은 값이 최대공약수
```javascript
function f(x,y){
              if(y==0){
                  return x;
              }else{
                  return f(y, x%y)
              }
          }

          console.log(f(20,12))
```

### 피보나치 수열
``` javascript
function fibonacci(n){
    if(n == 1 || n == 2){
        return 1;
    }

    return fibonacci(n-1) + fibonacci(n-2);
}
//f(f(f(f(2)+f(1))+f(2))+f(f(2)+f(1))) 
```