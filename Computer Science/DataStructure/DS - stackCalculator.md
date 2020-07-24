# 스택을 활용한 계산기 만들기

## 중위표기법
- 일반적으로 사람이 수식을 표기할 때 사용하는 표기법  
ex] 7 * 5 + 3

## 후위표기법
- 컴퓨터가 계산하기에 편한 수식의 형태
- 연산자가 뒤쪽에 위치  
ex] 7 5 * 3 +
 
 ## 스택을 활용해 수식을 계산하는 방법
 - 수식을 후위 표기법으로 변환합니다
 - 후위 표기법을 계산하여 결과를 도출합니다 

 ## 중위 표기법을 후위 표기법으로 바꾸는 방법
 - 피연산자가 들어오면 바로출력
 - 연산자가 들어오면 자기보다 우선순위가 높거나 같은 것들을 빼고 자신을 스택에 담는다
 - '('를 만나면 무조건 스택에 담는다
 - ')'를 만나면 '('를 만날 때까지 스택에서 출력

 ```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct {
	char data[100];
	struct Node* next;
} Node;

typedef struct {
	Node* top;
} Stack;

void push(Stack* stack, char* data) {
	Node* node = (Node*)malloc(sizeof(Node));
	strcpy(node->data, data);
	node->next = stack->top;
	stack->top = node;
}

char* getTop(Stack* stack) {
	Node* top = stack->top;
	return top->data;
}

char* pop(Stack* stack) {
	if (stack->top == NULL) {
		printf("스택 언더플로우가 발생했습니다.\n");
		return NULL;
	}
	Node* node = stack->top;
	char* data = (char*)malloc(sizeof(char) * 100);
	strcpy(data, node->data);
	stack->top = node->next;
	free(node);
	return data;
}

//----- 후위 표기법으로 변환 -----
// 우선순위 함수 만들기-> 순서가 높을수록 우선순위 높음
int getPriority(char* i) {
	if (!strcmp(i, "(")) return 0; 
	if (!strcmp(i, "+") || !strcmp(i, "-")) return 1;
	if (!strcmp(i, "*") || !strcmp(i, "/")) return 2;
	return 3;
}

// 변환함수 만들기
char* transition(Stack* stack, char** s, int size) {
	char res[1000] = "";
	for (int i = 0; i < size; i++) {
		if (!strcmp(s[i], "+") || !strcmp(s[i], "-") || !strcmp(s[i], "*") || !strcmp(s[i], "/")) {
			while (stack->top != NULL && getPriority(getTop(stack)) >= getPriority(s[i])) {
				strcat(res, pop(stack)); strcat(res, " ");
			}
			push(stack, s[i]);
		}
		else if (!strcmp(s[i], "(")) push(stack, s[i]);
		else if (!strcmp(s[i], ")")) {
			while (strcmp(getTop(stack), "(")) {
				strcat(res, pop(stack)); strcat(res, " ");
			}
		}
		else { strcat(res, s[i]); strcat(res, " "); }
	}	
	
	while (stack->top != NULL) {
		strcat(res, pop(stack)); strcat(res, " ");
	}
	
	return res;
	
}

// 계산기
void calculate(Stack* stack, char** s, int size) {
	int x, y, z;
	for (int i = 0; i < size; i++) {
		if (!strcmp(s[i], "+") || !strcmp(s[i], "-") || !strcmp(s[i], "*") || !strcmp(s[i], "/")) {
			x = atio(pop(stack));
			y = atoi(pop(stack));
			if (!strcmp(s[i], "+")) z = y + x;
			if (!strcmp(s[i], "-")) z = y - x;
			if (!strcmp(s[i], "*")) z = y * x;
			if (!strcmp(s[i], "/")) z = y / x;
			char buffer[100];
			sprintf(buffer, "%d", z);
			push(stack, buffer);

		}
		else {
			push(stack, s[i]);
		}
	}
	printf("%s\n", pop(stack));
}

int main(void) {
	Stack stack; 
	stack.top = NULL; 
	char a[100] = "( ( 3 + 4 ) * 5 ) - 5 * 7 * 5 - 5 * 10"; 
	int size = 1; 
	for (int i = 0; i < strlen(a); i++) { 
		if (a[i] == ' ') size++; } char* ptr = strtok(a, " "); 
		char** input = (char**)malloc(sizeof(char*) * size); 
		for (int i = 0; i < size; i++) { 
			input[i] = (char*)malloc(sizeof(char) * 100); 
		} 
		for (int i = 0; i < size; i++) { 
			strcpy(input[i], ptr); ptr = strtok(NULL, " "); 
		} 
		char b[1000] = ""; 
		strcpy(b, transition(&stack, input, size)); 
		printf("후위 표기법: %s\n", b);
	
		size = 1; for (int i = 0; i < strlen(b) - 1; i++) { // 마지막은 항상 공백이 들어가므로 1을 빼기 
			if (b[i] == ' ') size++; 
		} 
		char *ptr2 = strtok(b, " "); 
		for (int i = 0; i < size; i++) { 
			strcpy(input[i], ptr2); 
			ptr2 = strtok(NULL, " "); 
		} 
		calculate(&stack, input, size); 


	system("pause");
	return 0;
}

 ```
 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]