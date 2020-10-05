# 스택(Stack)

- 스택은 한쪽으로 들어가서 한쪽으로 나오는 자료구조
- 이러한 특성 때문에 수식 계산 등의 알고리즘에서 다방면으로 활용됨

- PUSH : 스택에 데이터를 넣는다
- POP : 스택에서 데이터를 빼낸다  

ex] 배열을 이용한 구현 방법 
```
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

#define SIZE 10000 
#define INF 999999

int stack[SIZE]; // 배열크기를 미리 할당해야하므로 메모리 낭비
int top = -1; // stack의 최상단(=입구) -> 맨오른쪽

void push(int data) { //stack에 값 넣기
	if (top == SIZE - 1) {
		printf("스택 오버플로우가 발생했습니다\n");
		return;
	}

	stack[++top] = data;
}

int pop() { // 값 뽑아내기
	if (top == -1) {
		printf("스택 언더플로우가 발생했습니다.\n");
		return -INF;
	}
	return stack[top--];
}

void show() { // 스택에 남아있는 전체값 출력
	printf("--- 스택의 최상단 --- \n");
	for (int i = top; i >= 0; i--) {
		printf("%d\n", stack[i]);
	}
	printf("--- 스택의 최하단 --- \n");
}

int main(void) {
	push(7);
	push(6);
	push(5);
	push(4);
	pop();
	push(3);
	show();
	
	system("pause");
	return 0;
}
```
> --- 스택의 최상단 ---  
> 3  
> 5  
> 6  
> 7  
> --- 스택의 최하단 ---     

ex] 연결리스트를 이용한 구현 방법
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

#define INF 999999

typedef struct {
	int data;
	struct Node* next;
	
} Node;

typedef struct {
	Node* top;
} Stack;

void push(Stack* stack, int data) {
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->next = stack->top;
	stack->top = node; // 마지막에 들어온 최상단 노드가 top
}

void pop(Stack *stack) { // 항상 최상단노드(top)을 삭제
	if (stack->top == NULL) {
		printf("스택 언더플로우가 발생했습니다.\n");
		return -INF;
	}

	Node* node = stack->top;
	int data = node->data;
	stack->top = node->next;
	free(node);
	return data;
}

void show(Stack* stack) {
	Node* cur = stack->top;
	printf("---스택의 최상단--- \n");
	while (cur != NULL) {
		printf("%d\n", cur->data);
		cur = cur->next;
	}
	printf("---스택의 최하단--- \n");

}

int main(void) {
	Stack s;
	s.top = NULL;

	push(&s, 7);
	push(&s, 5);
	push(&s, 4);
	pop(&s);
	push(&s, 6);
	pop(&s);
	show(&s);
	
	system("pause");
	return 0;
}
```
>---스택의 최상단---  
> 5  
> 7  
>---스택의 최하단---
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]
- 자료구조와 함께 배우는 알고리즘 입문 JAVA편