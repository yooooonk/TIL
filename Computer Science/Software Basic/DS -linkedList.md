# 연결리스트(Linked List)

## 연결리스트의 필요성
- 일반적으로 배열을 사용하는 데이터를 순차적으로 저장하고 나열할 수 있다
- 배열을 사용하는 경우 메모리 공간이 불필요하게 낭비될 수 있다

### _배열기반의 리스트_
- 데이터를 순자적으로 저장하고, 처리할 때
- 장점 : 배열로 만들었으므로 특정한 위치의 원소에 즉시 접근할 수 있다
- 단점 : 데이터가 들어갈 공간을 미리 메모리에 할당해야 한다, 원하는 위치로의 삽입이나 삭제가 비효율적
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#define INF 10000

int arr[INF];
int count = 0;

void addBack(int data) {
	arr[count] = data;
	count++;
}

void addFirst(int data) {
	for (int i = count; i >= 1; i--){
		arr[i] = arr[i - 1]; // 삽입할 때 배열값들을 한칸씩 뒤로 밀어줌
	}
	arr[0] = data;
	count++;
} 

void show() {
	for (int i = 0; i < count; i++) {
		printf("%d", arr[i]);
	}
}

void del(int v) { //특정 인덱스 삭제
	for (int i = v ; i < count; i++) {
		arr[i] = arr[i + 1];
	}
	count --;
}


int main(void) {
	addBack(1);
	addBack(2);
	addBack(3);
	addBack(4);
	addFirst(5);
	addFirst(6);
    del(2);
	show();
	system("pause");
	return 0;
}
```
### _연결 리스트_
- 일반적으로 구조체와 포인터를 함께 사용하여 구현한다
- 연결 리스트는 리스트 중간 지점에 노드를 추가하거나 삭제할 수 있어야 한다
- 필요할 때마다 메모리 공간을 할당 받는다
- 삽입과 삭제가 배열에 비해 간단하다
- 배열과 다르게 특정 인덱스로 즉시 접근하지 못하며, 원소를 차례대로 검색해야 한다
- 추가적인 포인터 변수가 사용되므로 메모리 공간이 낭비된다
- 예외 사항을 처리해줘야 한다  
 ex] 삭제할 원소가 없는데 삭제하는 경우, head 노드 자체를 잘못 넣은 경우 등
#### 단일연결 리스트
- 포인터를 이용해 단방향으로 다음 노드를 가리킴  
ex] data|next(Head) -> data|next(일반노드) -> data|next(일반노드) -> NULL
- 하나의 구조체 안에 두개의 변수 = 데이터를 받는 변수+다음 노드를 가리키는 포인터변수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct { //구조체
	int data;
	struct Node* next;
} Node;

Node* head;

// 값 삽입
void addFront(Node* root, int data) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->next = root->next;
	root->next = node;
}

// 값 삭제
void removeFront(Node *root) {
	Node* front = root->next;
	root->next = front->next;
	free(front);
}

//연결 리스트 메모리 해제 함수
void freeAll(Node* root) {
	Node* cur = head->next;
	while (cur != NULL)
	{
		Node* next = cur->next;
		free(cur);
		cur = next;
	}
}

void showAll(Node* root) {
	Node* cur = head->next;
	while (cur != NULL)
	{
		printf("%d ", cur->data);
		cur = cur->next;
	}
		
}

int main(void) {

	head = (Node*)malloc(sizeof(Node));

	head->next = NULL;
	
	addFront(head, 3);
	addFront(head, 2);
	addFront(head, 1);
	addFront(head, 1);
	removeFront(head);
	showAll(head);
	freeAll(head);

	system("pause");
	return 0;
}
```
=> 3 2 1
#### 양방향 연결 리스트
- 머리(Head)와 꼬리(Tail)을 모두 가진다
- 양방향 연결 리스트의 각 노드는 앞 노드와 뒤 노드의 정보를 모두 저장하고 있다
ex] prev|data|next(Head) <-> prev|data|next(일반노드) <-> prev|data|next(일반노드) <-> prev|data|next(Tail)
- 리스트의 앞뒤로 모두 접근할 수 있다
- 포인터가 두개가 사용되므로 메모리 공간이 조금 더 필요하다
ex]양방향 연결리스트 삽입 함수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct { //구조체
	int data;
	struct Node* prev;
	struct Node* next;	
} Node;

Node* head, * tail;

// 오름차순으로 값 삽입
void insert(int data) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	Node* cur;
	cur = head->next;
	while (cur->data < data && cur != tail)
	{
		cur = cur->next;
	}
	Node* prev = cur->prev;
	prev->next = node;
	node->prev = prev;
	cur->prev = node;
	node->next = cur;
}
// 가장 앞에 있는 값 삭제 
// head <-> node(삭제) <-> node2 <-> tail
void removeFront() {
	Node* node = head->next;
	head->next = node->next;
	Node* next = node->next;
	next->prev = head;
	free(node);
}

void show() {
	Node* cur = head->next;
	while (cur != tail) {
		printf("%d ", cur->data);
		cur = cur->next;
	}
}


int main(void) {
	head = (Node*)malloc(sizeof(Node));
	tail = (Node*)malloc(sizeof(Node));
	
	// head와 tail은 기본적으로 할당
	head->next = tail;
	head->prev = head;
	tail->next = tail;
	tail->prev = head;

	insert(3);
	insert(7);
	insert(5);
	insert(8);
	insert(9);
	insert(2);	
	removeFront();
	insert(1);
	show();
	
	system("pause");
	return 0;
}
```
=> 1 3 5 7 8 9