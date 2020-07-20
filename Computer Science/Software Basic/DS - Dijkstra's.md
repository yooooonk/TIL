# 다익스트라의 최단 경로 Dijkstra's Shortest Path Algorithm
- 각 간선에 대한 정보를 우선순위 큐에 담아 처리하는 방식으로 동작 원리가 프림 알고리즘과 흡사
- 다익스트라의 최단 경로 알고리즘은 음의 간선이 없을 때 정상적으로 동작함
- 현실 세계에서는 음의 간선이 존재하지 않기 때문에 다익스트라는 현실 세계에 적합한 알고리즘
1. 그래프의 시작점을 선택하여 트리 T에 포함시킴
2. T에 포함된 노드와 T에 포함되지 않은 노드 사이의 간선 중에서 '이동 거리'가 가장 작은 간선을 찾습니다.
3. 해당 간선에 연결된 T에 포함되지 않은 노드를 트리 T에 포함시킵니다
4. 모든 노드가 포함될 때까지 2와 3 과정을 반복합니다
``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define NODE_MAX	1001
#define EDGE_MAX	600001

typedef struct {
	int cost;
	int node;
} Edge;

void swap(Edge* a, Edge* b) {
	Edge temp;
	temp.cost = a->cost;
	temp.node = a->node;
	a->cost = b->cost;
	a->node = b->node;
	b->cost = temp.cost;
	b->node = temp.node;
}

typedef struct {
	Edge* heap[EDGE_MAX];
	int count;
} priorityQueue;
void push(priorityQueue* pq, Edge* edge) {
	if (pq->count >= EDGE_MAX) return;
	pq->heap[pq->count] = edge;
	int now = pq->count;
	int parent = (pq->count - 1) / 2;
	// 새 원소를 삽입한 이후에 상향식으로 힙을 구성합니다.
	while (now > 0 && pq->heap[now]->cost < pq->heap[parent]->cost) {
		swap(pq->heap[now], pq->heap[parent]);
		now = parent;
		parent = (parent - 1) / 2;
	}
	pq->count++;
}

Edge* pop(priorityQueue* pq) {
	if (pq->count <= 0) return NULL;
	Edge* res = pq->heap[0];
	pq->count--;
	pq->heap[0] = pq->heap[pq->count];
	int now = 0, leftChild = 1, rightChild = 2;
	int target = now;
	// 새 원소를 추출한 이후에 하향식으로 힙을 구성합니다.
	while (leftChild < pq->count) {
		if (pq->heap[target]->cost > pq->heap[leftChild]->cost) target = leftChild;
		if (pq->heap[target]->cost > pq->heap[rightChild]->cost && rightChild < pq->count) target = rightChild;
		if (target == now) break; // 더 이상 내려가지 않아도 될 때 종료
		else {
			swap(pq->heap[now], pq->heap[target]);
			now = target;
			leftChild = now * 2 + 1;
			rightChild = now * 2 + 2;
		}
	}
	return res;
}
// 프림 알고리즘 간선 연결 리스트 구현
typedef struct Node {
	Edge* data;
	struct Node* next;
} Node;
Node** adj;
int ans[NODE_MAX];
void addNode(Node** target, int index, Edge* edge) {
	if (target[index] == NULL) {
		target[index] = (Node*)malloc(sizeof(Node));
		target[index]->data = edge;
		target[index]->next = NULL;
	}
	else {
		Node* node = (Node*)malloc(sizeof(Node));
		node->data = edge;
		node->next = target[index];
		target[index] = node;
	}
}
// 프림 알고리즘 사용해보기
int main(void) {
	int n, m, k;
	scanf("%d %d %d", &n, &m, &k);
	adj = (Node**)malloc(sizeof(Node*) * (n + 1));
	for (int i = 1; i <= n; i++) {
		adj[i] = NULL;
		ans[i] = INT_MAX;
	}
	priorityQueue* pq;
	pq = (priorityQueue*)malloc(sizeof(priorityQueue));
	pq->count = 0;
	for (int i = 0; i < m; i++) {
		int a, b, c;
		scanf("%d %d %d", &a, &b, &c);
		Edge* edge = (Edge*)malloc(sizeof(Edge));
		edge->node = b;
		edge->cost = c;
		addNode(adj, a, edge);
	}
}
```