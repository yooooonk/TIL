# 우선순위 큐 Priority Queue
- '우선순위'를 가진 데이터들을 저장하는 큐
- 큐는 FIFO.우선순위 큐는 우선순위가 가장 높은 데이터가 가장 먼저 나옴
- 운영체제의 작업 스케줄링, 정렬, 네트워크 관리 등의 다양한 기술에 적용
- 큐는 선형적 구조, 우선순위 큐는 이진트리 구조로 본다
- 최대힙을 이용해 구현
- 우선순위 큐의 삽입과 삭제는 O(logN)의 시간 복잡도를 가짐
#### 최대 힙 Max Heap
- <u>부모노드</u>가 자식보다 보다 <u>값이 큰</u> <u>완전이진트리</u>
- 삽입 : 삽입 후에 루트 노드까지 거슬러 올라가 최대 힙을 구성(상향식)
- 삭제 : 루트 노드를 삭제하고, 가장 마지막 원소를 루트 노드의 위치로 옮겨준다(하향식)
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define MAX_SIZE 10000

void swap(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

typedef struct {
	int heap[MAX_SIZE];
	int count;
} priorityQueue;

void push(priorityQueue* pq, int data) {
	if (pq->count >= MAX_SIZE) return;
	pq->heap[pq->count] = data;
	int now = pq->count;
	int parent = (pq->count - 1) / 2; // ???
	// 새 원소를 삽입한 이후에 상향식으로 힙을 구성
	while (now > 0 && pq->heap[parent] > pq->heap[parent]) {
		swap(&pq->heap[now], &pq->heap[parent]);
		now = parent;
		parent = (parent - 1) / 2;
	}
	pq->count++;	
}

int pop(priorityQueue* pq) {
	if (pq->count <= 0) return -9999;
	int res = pq->heap[0];
	pq->count--;
	pq->heap[0] = pq->heap[pq->count];
	int now = 0, leftChild = 1, rightChild = 2;
	int target = now;
	// 새 원소를 추출한 이후 하향식으로 힙을 구성
	while (leftChild < pq->count) {
		if (pq->heap[target] < pq->heap[leftChild]) target = leftChild;
		if (pq->heap[target] < pq->heap[rightChild] && rightChild < pq->count) target = rightChild;
		if (target == now) break; // 더 이상 내려가지 않아도 될 때 종료
		else {
			swap(&pq->heap[now], &pq->heap[target]);
			now = target;
			leftChild = now * 2 + 1;
			rightChild = now * 2 + 2;
		}
	}
	return res;
}

int main(void) {
	int n, data; 
	scanf("%d", &n);
	priorityQueue pq;
	pq.count = 0;
	for (int i = 0; i < n; i++) {
		scanf("%d ", & data);
		push(&pq, data);
	}
	for (int i = 0; i < n; i++) {
		int data = pop(&pq);
		printf("%d ", data);
	}

	system("pause");
	return 0;
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]