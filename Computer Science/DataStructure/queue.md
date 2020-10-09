# 큐(Queue)
- 뒤쪽으로 들어가서 앞쪽으로 나오는 자료 구조
- 가장 먼저 너은 데이터를 가장 먼저 꺼내는 선입선출 구조(FIFO)
- 스케줄링, 탐색 알고리즘 등에서 다방면을 활용
- push : 큐에 데이터를 넣음
- pop : 데이터를 빼냄
![queue](https://github.com/yooooonk/TIL/blob/master/img/queue.png)

### 배열을 이용한 큐 구현
``` java
import sun.invoke.empty.Empty;

class Queue{
    private int max;
    private int num;
    private int[] que;

    public Queue(int max){
        this.max = max;
        num = 0;
        try {
            que = new int[max];    
        } catch (OutOfMemoryError e) {
            max = 0;
        }
        
    }

    public class EmptyQueException extends RuntimeException{
        public EmptyQueException(){}
    }

    public class OverflowQue extends RuntimeException{
        public OverflowQue(){}
    }

    public int enQue(int n) throws OverflowQue{
        if(num >= max){
            throw new OverflowQue();
        }

        return que[num++] =  n;
    }

    public int deQue() throws EmptyQueException{
        if(num <= 0){
            throw new EmptyQueException();
        }

        int dQue = que[0];

        for(int i = 0; i < num-1 ; i++){
            que[i] = que[i+1];            
        }
        num --;
        
        return dQue;
    }

    public int peek() throws EmptyQueException{
        if(num <= 0){
            throw new EmptyQueException();
        }

        return que[num-1];
    }

    public int indexOf(int x){
        for(int i = 0; i< num ; i++){
            if(que[i]==x){
                return i;
            }
        }
        return -1;
    }

    public void clear(){
        num = 0;
    }

    public int capacity(){
        return max;
    }

    public int size(){
        return num;
    }

    public boolean isFull(){
        return num >= max;
    }

    public boolean isEmpty(){
        return num<=0;
    }

    public void dump(){
        if(num <= 0){
            System.out.println("큐가 비었습니다아아");
        }else{
            for(int i = 0 ; i< num ; i++){
                System.out.print(que[i]+" ");
            }
            System.out.println();
        }

    }
}\

```
### 링 버퍼로 큐 구현
- 배열 요소를 앞쪽으로 옮기지 않는 큐
- 배열의 처음과 끝이 연결되어있다고 보는 자료구조
- 논리적으로 어떤 요소가 첫 번째 요소이고 어떤 요소가 마지막 요소인지 식별하기 위한 변수가 front와 rear
	- front : 맨 처음 요소의 인덱스
	- rear : 맨 끝 요소의 하나 뒤의 인덱스(다음 요소를 인큐할 위치를 미리 지정)

 ### 연결 리스트를 이용한 큐 구현
 ``` java
class IntQueue{
    private int max;
    private int front; // 첫
    private int rear; // 끝
    private int num; // 현재 데이터 수
    private int[] que;

    public class EmptyQueueException extends RuntimeException{
        public EmptyQueueException(){}
    }

    public class OverFlowQueueException extends RuntimeException{
        public OverFlowQueueException(){}
    }

    public IntQueue(int capacity){
        num = front = rear = 0;
        max = capacity;
        try {
            que = new int[max];
        } catch (OutOfMemoryError e) {
            max = 0;
        }
    }

    public int enque(int x) throws OverFlowQueueException{
        if(num >= max){
            throw new OverFlowQueueException();
        }

        que[rear++] = x;
        num++;

        if(rear == max){
            rear = 0;
        }
        return x;
    }

    public int deque() throws EmptyQueueException{
        if(num <= 0){
            throw new EmptyQueueException();
        }

        int x = que[front++];
        num --;

        if(front == max){
            front = 0;
        }
        return x;
    }

    public int peek() throws EmptyQueueException{
        if(num <= 0){
            throw new EmptyQueueException();
        }

        return que[front];
    }

    public int indexOf(int x){
        for(int i = front ; i< rear ; i++){
            //int idx = (i+front) % max;
            if(que[i]==x){
                return i;
            }
        }
        return -1;
    }

    public void clear(){
        num = front = rear = 0;
    }

    public int capacity(){
        return max;
    }

    public int size(){
        return num;
    }

    public boolean isEmpty(){
        return num <= 0;
    }

    public boolean isFull(){
        return num >= max;
    }

    public void dumb(){
        if(num<=0){
            System.out.println("큐가 비어 있습니다");
        }else{
            for(int i = 0; i <num; i++){
                System.out.println(que[(i+front)%max]+" ");
            }
            System.out.println();
        }        
    }
}

 ```
 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- &#128214; [자료구조와 함께 배우는 알고리즘 입문 JAVA편]
- https://www.studytonight.com/data-structures/queue-data-structure