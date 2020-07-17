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