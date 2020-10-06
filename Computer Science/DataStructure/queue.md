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

 ### 연결 리스트를 이용한 큐 구현
 ``` c
 #define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define SIZE 10000
#define INF 9999999

typedef struct {
	int data;
	struct Node* next;
} Node;

typedef struct {
	Node* front;
	Node* rear;
	int count;
}Queue;

void push(Queue* q, int data) { // 새 노드가 rear
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->next = NULL;
	if (q->count == 0) {
		q->front = node;
	}
	else {
		q->rear->next = node;
	}

	q->rear = node;
	q->count++;
}

void pop(Queue* q) { // front를 삭제, 그 다음 노드가 front
	if (q->count ==0) { 
		printf("큐 언더플로우가 발생했습니다 \n");
		return -INF;
	}
	
	Node* node = q->front;
	int data = node->data;
	q->front = node->next;
	free(node);
	q->count--;
	return data;
}

void show(Queue* q) {
	Node* cur = q->front;
	printf("--큐의 앞--\n");
	while (cur != NULL){
		printf("%d\n", cur->data);
		cur = cur->next;
	}
	printf("--큐의 뒤--");
}

int main(void) {
	
	Queue q;
	q.front = q.rear = NULL;
	q.count = 0;

	push(&q, 7);
	push(&q, 5);
	push(&q, 4);
	pop(&q);
	push(&q, 6);
	pop(&q);
	show(&q);
	
	system("pause");
	return 0;
}
 ```
 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- [자료구조와 함께 배우는 알고리즘 입문 JAVA편]
- https://www.studytonight.com/data-structures/queue-data-structure