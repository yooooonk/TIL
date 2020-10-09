# 스택(Stack)

- 데이터를 일시적으로 저장하기 위해 사용하는 자료구조로 가장 나중에 넣은 데이터를 가장 먼저 꺼냄(LIFO)
- 스택은 한쪽으로 들어가서 한쪽으로 나오는 자료구조
- 이러한 특성 때문에 수식 계산 등의 알고리즘에서 다방면으로 활용됨

- PUSH : 스택에 데이터를 넣는다
- POP : 스택에서 데이터를 빼낸다  
![stack](https://github.com/yooooonk/TIL/blob/master/img/stack.png)

ex] 배열을 이용한 구현 방법 
``` java
class intStack{
    int max; //스택 용량
    int ptr; // 스택 포인터 : 스택에 쌓여 있는 데이터 수 
    int[] stk; // 스택 본체

    // 예외 : 스택이 비어있음
    public class EmptyIntStackException extends RuntimeException{
        public EmptyIntStackException(){}
    }

    // 예외 : 스택이 가득 참
    public class OverflowIntStackException extends RuntimeException{
        public OverflowIntStackException(){}
    }

    //생성자
    public intStack(int capacity){
        prt = 0;
        max = capacity;
        try{
            stk = new int[max];
        }catch(OutOfMemoryError e){
            max = 0;
        }
    }

    // 푸쉬
    public int push(int x) throws OverflowIntStackException{
        if(prt>=max){
            throw new OverflowIntStackException();           
        }
        return stk[ptr++] = x; 
    }

    //팝
    public int pop() throws EmptyIntStackException{
        if(ptr<=0){
            throw new EmptyIntStackException();
        }

        return stk[prt--];
    }

    //peek
    public int peek() throws EmptyIntStackException{
        if(ptr<=0){
            throw new EmptyIntStackException();
        }

        return stk[ptr-1];
    }

    // 검색 메서드 index of
    public int indexOf(int x){
        for(int i= ptr-1 ; i>=0 ; i--){
            if(stk[i] == x){
                return i;
            }           
        }
        return -1;
    }

    // 스택을 비움
    public void clear(){
        ptr = 0;
    }

    // 스택의 용량을 반환
    public int capacity(){
        return max;
    }

    // 스택에 쌓여 있는 데이터 수를 반환
    public int size(){
        return ptr;
    }

    // 비어있는가?
    public boolean isEmpty(){
        return ptr<=0;
    }

    // 가득찼는가?
    public boolean isFull(){
        return ptr >= max;
    }

    // 스택의 모든 데이터를 바닥->꼭대기 순서로 출력
    public void dump(){
        if(ptr<=0){
            System.out.println("스택이 비어있습니다");
        }else{
            for(int i = 0; i<ptr ; i++){
                System.out.print(stk[i]+" ");
            }
            System.out.println();
        }

    }
}

```

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
- &#128214;[자료구조와 함께 배우는 알고리즘 입문 JAVA편]
- stack img https://www.programiz.com/dsa/stack