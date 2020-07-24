# 선택정렬(Selection Sort)
- 선택 정렬이란 가장 작은 것을 선택해서 앞으로 보내는 정렬기법
- 가장 작은 것을 선택하는 데에 N번, 앞으로 보내는 데에 N번의 연산으로 O(N²)의 시간 복잡도를 가진다                  
 

### 선택정렬 구현
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <limits.h>

#define SIZE 1000

int a[SIZE];

int swap(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

int main(void) {
	
	int n, min, index;
	scanf("%d", &n); // 원소개수
	for (int i = 0; i < n; i++) {
		scanf("%d", &a[i]); // 입력한 숫자 읽기
	}
	for (int i = 0; i < n; i++) {
		min = INT_MAX;
		for (int j = i; j < n; j++) {
			if (min > a[j]) {
				min = a[j];
				index = j; // 가장 작은 값이 존재하는 위치
			}
		}
		swap(&a[i], &a[index]);
	}

	for (int i = 0; i < n; i++) {
		printf("%d", a[i]);
	}
	
	system("pause");
	return 0;
}
```

 # 삽입정렬(Insertion Sort)
- 삽입 정렬이란 각 숫자를 적절한 위치에 삽입하는 정렬기법
- 들어갈 위치를 선택하는 데에 N번, 선택한 횟수로 N번이므로 O(N²)의 시간 복잡도를 가진다                          
 

### 선택정렬 구현
``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <limits.h>

#define SIZE 1000

int a[SIZE];

int swap(int* a, int* b) {
	int temp = *a;
	*a = *b;
	*b = temp;
}

int main(void) {
	
	int n, min, index;
	scanf("%d", &n); // 원소개수
	for (int i = 0; i < n; i++) {
		scanf("%d", &a[i]); // 입력한 숫자 읽기
	}
	for (int i = 0; i < n - 1; i++) {
		int j = i;
		while (j >= 0 && a[j] > a[j + 1]) {
			
		}
	}

	for (int i = 0; i < n; i++) { //출력
		printf("%d", a[i]);
	}
	
	system("pause");
	return 0;
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]