# 순차 탐색 Sequential Search
- 특정한 원소를 찾기 위해 원소를 순차적으로 하나씩 탐색하는 방법
- 데이터 정렬 유무에 상관없이 가장 앞에 있는 원소부터 하나씩 확인해야 한다는 점에서 O(N)의 시간 복잡도

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define LENGTH 1000

char** array;
int founded; // 특정원소를 발견했는지

// 문자열 순차 탐색 알고리즘
int main(void) {
	int n;
	char* word;
	word = malloc(sizeof(char) * LENGTH);
	scanf("%d %s", &n, word);
	array = (char**)malloc(sizeof(char*) * n);
	for (int i = 0; i < n; i++) {
		array[i] = malloc(sizeof(char) * LENGTH);
		scanf("%s", array[i]);
	}
	for (int i = 0; i < n; i++) {
		if (!strcmp(array[i], word)) {
			printf("%d번째 원소입니다.\n", i + 1);
			founded = 1;
		}
	}

	if (!founded) printf("원소를 찾을 수 없습니다.\n");
	
	system("pause");
	return 0;
}
```

# 이진 탐색 Binary Search
- 내부 데이터가 이미 정렬 되어 있는 상황에서 사용 가능한 알고리즘
- 탐색 범위를 절반씩 좁혀가며 데이터를 탐색 -> O(logN)의 시간 복잡도
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_SIZE 10000

int a[MAX_SIZE];
int founded = 0;

int search(int start, int end, int target) {
	if (start > end) return -9999;
	int mid = (start + end) / 2;
	if (a[mid] == target) return mid;
	else if (a[mid] > target) return search(start, mid - 1, target);
	else return search(mid + 1, end, target); 
}

int main(void) {
	int n, target;
	scanf("%d %d", &n, &target);
	
	for (int i = 0; i < n; i++) scanf("%d", &a[i]);
	int result = search(0, n - 1, target);
	if (result != -9999) printf("%d번째 원소입니다.\n", result + 1);
	else printf("원소를 찾을 수 없습니다.\n");
		
	system("pause");
	return 0;
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]