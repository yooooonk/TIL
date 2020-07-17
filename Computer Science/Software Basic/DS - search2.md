# 깊이 우선 탐색 Depth First Search
- 깊은 것을 우선적으로 탐색하는 알고리즘
- 전체 노드를 맹목적으로 탐색하고자 할 때 사용
- Stack 자료구조를 기초로한다
- 모든 경우의 수를 빠르게 탐색하고자 할 때 쉽게 사용할 수 있다
- 탐색 시작 노트를 스택에 삽입하고 방문처리 ->  
스택의 최상단 노드에게 방문하지 않은 인접 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리.   
방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다 -> 이걸 못할때까지 반복
- O(N)의 시간복잡도
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 1001

// 연결 리스트 정의
typedef struct {
	int index;
	struct Node* next;
}Node;

Node** a; // 정점이 여러개
int n, m, c[MAX_SIZE];

// 연결리스트 삽입함수
void addFront(Node* root, int index) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->index = index;
	node->next = root->next;
	root->next = node;
}

// 깊이 우선 탐색 함수
void dfs(int x) {
	if (c[x]) return; //해당노드를 방문한 적이 있다면 바로 return
	c[x] = 1; //방문처리
	printf("%d ", x); // 해당 노드 출력
	Node* cur = a[x]->next;
	while (cur != NULL) {
		int next = cur->index; // 연결되어 있는 노드
		dfs(next); //재귀호출
		cur = cur->next;
	}
}


int main(void) {
	scanf("%d %d", &n, &m);
	a = (Node**)malloc(sizeof(Node*) * (MAX_SIZE)); //정점의 갯수만큼 할당
	for (int i = 1; i <= n; i++) { // 초기화
		a[i] = (Node*)malloc(sizeof(Node));
		a[i]->next = NULL;
	}
	for(int i = 0;i<m;i++){ // 간선의 갯수만큼 연결
		int x, y;
		scanf("%d %d", &x, &y);
		addFront(a[x], y);
		addFront(a[y], x);
	}

	dfs(1);
	system("pause");
	return 0;
}
```

# 너비 우선 탐색 Breadth First Search
- 너비를 우선으로 하여 탐색을 수행하는 탐색 알고리즘
- DFS와 같이 맹목적으로 전체 노드를 탐색하고자 할 때 자주 사용
- Queue 자료구조를 기로로 한다
- 고급 그래프 탐색 알고리즘에서 자주 활용되므로 고급 개발자가 되기 위해서는 너비 우선 탐색에 대해 숙지해야한다 
- 탐색 시작 노드를 큐에 넣고 방문 처리 ->  
큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드들을 모두 큐에 삽입하고 방문처리->  
반복
- O(N)의 시간복잡도, 일반적인 경우 실제 수행 시간은 DFS보다 좋은 편
``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#define MAX_SIZE 1001
#define INF 999999

// 연결 리스트 정의
typedef struct {
	int index;
	struct Node* next;
}Node;

Node** a; // 정점이 여러개
int n, m, c[MAX_SIZE];

// 큐
typedef struct {
	Node* front;
	Node* rear;
	int count;
} Queue;

Node** a;
int n, m, c[MAX_SIZE];

// 연결 리스트 삽입 함수
void addFront(Node* root, int index) {
	Node* node = (Node*)maooloc(sizeof(Node));
	node->index = index;
	node->next = root->next;
	root->next = node;
}

// 큐 삽입함수
void pushQ(Queue* q, int index) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->index = index;
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

// 큐 추출함수
int popQ(Queue* q) {
	if(q->count ==0){
		printf("큐 언더플로우가 발생했습니다.\n")
			return -INF;
	}
	Node* node = q->front;
	int index = node->index;
	q->front = node->next;
	free(node);
	q->count--;
	return index;
}

// 너비 탐색함수
void bfs(int start) {
	Queue q;
	q.front = q.rear = NULL;
	q.count = 0;
	pushQ(&q, start); // 첫탐색 인덱스 넣음
	c[start] = 1; // 방문처리
	while (q.count != 0) {
		int x = popQ(&q);
		printf("%d ", x);
		Node* cur = a[x]->next;
		while (cur != NULL) {
			int next = cur->index; //인접한 노드
			if (!c[next]) { // 방문하지 않았다면
				pushQ(&q, next); // 큐에 넣고
				c[next] = 1; // 방문처리
			}
			cur = cur -> next;
		}
	}
}


int main(void) {
	scanf("%d %d", &n, &m); // 정점, 간선
	a = (Node**)malloc(sizeof(Node*) * (MAX_SIZE)); //정점의 갯수만큼 할당
	for (int i = 1; i <= n; i++) { // 연결리스트 초기화
		a[i] = (Node*)malloc(sizeof(Node));
		a[i]->next = NULL;
	}
	for(int i = 0;i<m;i++){  // 간선의 갯수만큼 연결
		int x, y;
		scanf("%d %d", &x, &y);
		addFront(a[x], y);
		addFront(a[y], x);
	}

	bfs(1);
	system("pause");
	return 0;
}
```