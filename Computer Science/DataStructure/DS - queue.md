# 큐(Queue)
- 뒤쪽으로 들어가서 앞족으로 나오는 자료 구조
- 스케줄링, 탐색 알고리즘 등에서 다방면을 활용
- push : 큐에 데이터를 넣음
- pop : 데이터를 빼냄

### 배열을 이용한 큐 구현
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define SIZE 10000
#define INF 9999999

int queue[SIZE];
int front = 0;
int rear = 0;

void push(int data) {
	if (rear >= SIZE) {
		printf("큐 오버플로우가 발생했습니다.\n");
		return;
	}

	queue[rear++] = data;
}

void pop() {
	if (front == rear) {
		printf("큐 언더플로우가 발생했습니다 \n");
		return -INF;
	}
	return queue[front++];
}

void show() {
	printf("--큐의 앞--\n");
	for (int i = front; i <= rear; i++) {
		printf("%d\n", queue[i]);
	}
	printf("--큐의 뒤--");
}

int main(void) {
	
	push(7);
	push(5);
	push(4);
	pop();
	push(6);
	pop();
	show();	

	system("pause");
	return 0;
}
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