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