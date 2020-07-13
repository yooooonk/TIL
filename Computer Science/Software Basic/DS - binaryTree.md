# 트리 Tree
- Tree : 나무의 형태를 뒤집은 것과 같은 형태의 자료구조
- 루트노드(트리의 최상단) - 가지 - 리프노드(트리구조의 맨끝)
- 루트(부모) - 리프(자식), 리프(형제) - 리프(형제)
- 길이(length) : 출발 노드에서 목적지 노드까지 거쳐야 하는 가짓수
- 깊이(depth) : 루트 노드에서 특정 노드까지의 길이
- 높이(Height) : 루트 노드에서 가장 깊은 노드까지의 길이

# 이진트리 Binary Tree
- 최대 2개의 자식을 가질 수 있는 트리
- 많은 양의 노드를 낮은 높이에서 관리할 수 있으므로 데이터 활용의 효율성이 높다
- 데이터 저장, 탐색 등 다양한 목적으로 사용
- 종류
1. 포화 이진 트리(Full Binary Tree) : 리프 노드를 제외한 모든 노드가 두 자식을 가지고 있는 트리
2. 완전 이진트리(Complete Binary Tree) : 모든 노드들이 왼쪽부터 채워진 이진트리
3. 높이균형 트리(Height Balanced Tree) : 왼쪽 자식트리와 오른쪽 자식트리의 높이가 1이상 차이나지 않는 트리  

### 이진 트리의 순회
- 이진 트리에 담긴 데이터를 하나씩 방문하는 방법
1. 전위순회 : 자기 자신을 출력 -> 왼쪽 자식 방문 -> 오른쪽 자식 방문
2. 중위순회 : 왼쪽 자식 방문 -> 자기자신 출력 -> 오른쪽 자식 방문 => 왼쪽에서 부터 차례대로 출력하는 결과
3. 후위순회 : 왼쪽 자식 방문 -> 오른쪽 자식 방문 -> 자기 자신 출력 => 루트가 가장 마지막으로
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct {
	int data; // 실제로는 정수형 한개보다 더 많은 양의 데이터가 들어갈 수 있음.
	struct Node* leftChild;
	struct Node* rightChild;
} Node;

Node* initNode(int data, Node* leftChild, Node* rightChild) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->leftChild = leftChild;
	node->rightChild = rightChild;
	return node;
}

// 전위 순회
void preorder(Node* root) {
	if (root) { // node가 널이 아니라면
		printf("%d ", root->data);
		// 재귀호출
		preorder(root->leftChild);
		preorder(root->rightChild); 
	}
}

// 중위 순회
void inorder(Node* root) {
	if (root) {
		inorder(root->leftChild);
		printf("%d ", root->data);
		inorder(root->rightChild);
	}
}

// 후위 순회
void postorder(Node* root) {
	if (root) {
		inorder(root->leftChild);		
		inorder(root->rightChild);
		printf("%d ", root->data);
	}
}

int main(void) {
	Node* n7 = initNode(50, NULL, NULL);
	Node* n6 = initNode(37, NULL, NULL);
	Node* n5 = initNode(23, NULL, NULL);
	Node* n4 = initNode(5, NULL, NULL);
	Node* n3 = initNode(48, n6, n7);
	Node* n2 = initNode(17, n4, n5);
	Node* n1 = initNode(30, n2, n3);

	preorder(n1);
	printf("\n");
	inorder(n1);
	printf("\n");
	postorder(n1);
	printf("\n");
}
```