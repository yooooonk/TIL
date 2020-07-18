# AVL 트리 AVL Tree
- 균형이 갖춰진 이진 트리
- 간단한 구현 과정으로 특정 이진 트리가 완전 이진 트리에 가까운 형태를 유지하도록 해줌
- 균형 인수(Balance Factor) = |왼쪽 자식 높이 - 오른쪽 자식 높이|
- 모든 노드에 대한 균형인수가 +1, 0, -1
- 균형 인수가 세 가지에 해당하지 않는 경우 '회전(rotation)'을 통해 트리를 재구성해야 함
- 균형 인수가 깨지는 경우 (균형 인수가 깨진 노드를 X라고 함)
	1. LL형식 : X의 왼쪽 자식의 왼쪽에 삽입
	2. LR형식 : X의 왼쪽 자식의 오른쪽에 삽입
	3. RR형식 : X의 오른쪽 자식의 오른쪽에 삽입
	3. RL형식 : X의 오른쪽 자식의 왼쪽에 삽입
- AVL 트리의 각 노드는 '균형 인수'를 계산하기 위한 목적으로 자신의 높이값을 가짐
- AVL 트리의 균형 잡기는 각 노드가 '삽입 될 때'마다 수행되어야 한다.
- '삽입' 과정에 소요되는 시간 복잡도는 O(logN). 따라서 각 트리의 균형 잡기는 삽입 시에 거치는 모든 노드에 대하여 수행된다는 점에서 O(1)의 시간 복잡도를 만족해야한다

``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>


int getMax(int a, int b) {
	if (a > b) return a;
	return b;
}

// AVL트리 정의
typedef struct {
	int data;
	int height;
	struct Node* leftChild;
	struct Node* rightChild;

}Node;

// 특정 노드의 높이값
int getHeight(Node* node) {
	if (node == NULL) return 0;
	return node->height;
}

// 모든 노드는 회전을 수행한 이후 높이를 다시 계산
void setHeight(Node* node) {
	node->height = getMax(getHeight(node->leftChild), getHeight(node->rightChild)) + 1;
}

int getDifference(Node* node) {
	if (node == NULL) return 0;
	Node* leftChild = node->leftChild;
	Node* rightChild = node->rightChild;
	return getHeight(leftChild) - getHeight(rightChild);
}

// LL회전
Node* rotateLL(Node* node) {
	Node* leftChild = node->leftChild;
	node->leftChild = leftChild->rightChild;
	leftChild->rightChild = node;
	setHeight(node); // 회전 이후 높이를 다시 계싼
	retrun leftChild; 
}

// RR회전
Node* rotateRR(Node* node) {
	Node* rightChild = node->rightChild;
	node->rightChild = rightChild->leftChild;
	rightChild->leftChild = node;
	setHeight(node); // 회전 이후 높이를 다시 계싼
	retrun rightChild;
}

// LR회전
Node* rotateLR(Node* node) {
	Node* leftChild = node->leftChild;
	node->leftChild = rorateRR(leftChild);
	setHeight(node->leftChild);
	return rotateLL(node);  
}

// RL회전
Node* rotateRL(Node* node) {
	Node* rightChild = node->rightChild;
	node->rightChild = rorateLL(rightChild);
	setHeight(node->rightChild);
	return rotateLL(node);
}

// 균형잡기
Node* balance(Node* node) {
	int difference = getDifference(node);
	if (difference >= 2) {
		if(getDifference(node->leftChild) >= 1) {
			node = rotateLL
			(node);
		}else{
			node = rotateLR
			(node);
		}
	}
	else if (difference <=-2) {
		if(getDifference(node-> rightChild) <=-1) {
			node = rotateRR
			(node);
		}else{
			node = rotateRL
			(node);
		}
	}
	setHeight(node); // 회전 이후에 높이를 다시 계산
	return node	;
}

// 삽입
Node* insertNode(Node* node, int data) {
	if (!node) {
		node = (Node*)malloc(sizeof(Node));
		node->data = data;
		node->height = 1;
		node->leftChild = node->rightChild = NULL;
	}
	else if (data < node->data) {
		node->leftChild = insertNode(node->leftChild, data);
		node = balance(node);
	}
	else if (data > node->data) {
		node->rightChild = insertNode(node->rightChild, data);
		node = balance(node);
	}
	else {
		printf("데이터 중복이 발생했습니다.\n");
	}
	return node;
}

// 출력
Node* root = NULL;
void display(Node* node, int level) {
	if (node != NULL) {
		display(node->rightChild, level + 1);
		printf("\n");
		if (node == root) {
			printf("Root: ");
		}
		for (int i = 0; i < level && node != root; i++) {
			printf(" ");
		}
		printf("%d(%d)", node->data, getHeight(node));
		display(node->leftChild, level + 1);
	}
}

int main(void) {
	root = insertNode(root, 7);
	root = insertNode(root, 6);
	root = insertNode(root, 5);
	root = insertNode(root, 3);
	root = insertNode(root, 1);
	root = insertNode(root, 9);
	root = insertNode(root, 8);
	root = insertNode(root, 12);
	root = insertNode(root, 16);
	root = insertNode(root, 18);
	root = insertNode(root, 23);
	root = insertNode(root, 21);
	root = insertNode(root, 14);
	root = insertNode(root, 15);
	root = insertNode(root, 19);
	root = insertNode(root, 20);
	display(root, 1); 
	printf("\n");
	
	system("pause");
}
```

