# 트리의 효율성
- 데이터의 개수가 N개 일 때 배열과 마찬가지로 O(N)의 공간만이 소요
- 일반적인 경우 삽입, 삭제가 Array를 이용한 방식보다 효율적
- 그래서 데이터베이스 등 대용량 저장 및 검색 자료구조로 많이 활용됨

# 이진 탐색 트리 Binary Search Tree
- 이진 탐색이 항상 동작하도록 구현하여 탐색 속도를 극대화 시킨 자료구조
- 부모 노드가 항상 왼쪽 자식보다는 크고, 오른쪽 자식보다는 작다
- O(logN)의 시간 복잡도
- 찾고자 하는 값이 부모 노드보다 작을 경우 왼쪽 자식으로, 찾고자 하는 값이 부모 노드보다 클 경우 오른쪽 자식으로 이어 나가면서 방문
- 성능을 최대로 끌어내기 위해서는 이진 탐색 트리가 **_완전 이진탐색 트리_** 에 가까워 질 수 있도록 설계해야 함
- 한쪽으로 치우친 편향 이진 트리(Skewed Binary Tree)는 O(N)의 시간복잡도를 가지므로 Array를 사용하는 것보다 더 많은 시간과 공간을 낭비한다
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>


// 이진 탐색 트리
typedef struct {
	int data;
	struct Node* leftChild;
	struct Node* RightChild;
}Node;



// 이진 트리 삽입 함수
Node* insertNode(Node* root, int data) {
	if (root == NULL) {
		root = (Node*)malloc(sizeof(Node));
		root->leftChild = root->RightChild = NULL;
		root->data = data;
		return root;
	}
	else {
		if (root->data > data) {
			root->leftChild = insertNode(root->leftChild, data);
		}
		else {
			root->RightChild = insertNode(root->RightChild, data);
		}
	}
	return root;
}

// 탐색
Node* searchNode(Node* root, int data) {
	if (root == NULL) return NULL;
	if (root->data == data) return root;
	else if (root->data > data) return searchNode(root->leftChild, data);
	else return searchNode(root->RightChild, data);
}

// 이진 탐색 트리의 순회
void preorder(Node* root) {
	if (root == NULL) return;
	printf("%d ", root->data);
	preorder(root->leftChild);
	preorder(root->RightChild);
}

// 이진 탐색 트리의 가장 작은 원소 찾기 함수
Node* findMinNode(Node* root) {
	Node* node = root;
	while (node->leftChild != NULL) {
		node = node->leftChild;
	}
	return node;
}

//삭제함수
Node* deleteNode(Node* root, int data) {
	Node* node = NULL;
	if (root == NULL) return NULL;
	if (root->data > data) root->leftChild = deleteNode(root->leftChild, data);
	else if (root->data < data) root->RightChild = deleteNode(root->RightChild, data);
	else {
		if (root->leftChild != NULL && root->RightChild != NULL) {
			node = findMinNode(root->RightChild);
			root->data = node->data;
			root->RightChild = deleteNode(root->RightChild, node->data);
		}
		else {
			node = (root->leftChild != NULL) ? root->leftChild : root->RightChild;
			free(root);
			return node;
		}
	}
	return node;
}

int main(void) {
	Node* root = NULL;
	root = insertNode(root, 30);
	root = insertNode(root, 17);
	root = insertNode(root, 48);
	root = insertNode(root, 5);
	root = insertNode(root, 23);
	root = insertNode(root, 37);
	root = insertNode(root, 50);
	preorder(root);

	system("pause");
	return 0;
}
```

