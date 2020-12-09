# 계수정렬(Counting sort)
- 크기를 기준으로 데이터의 개수를 세는 정렬 알고리즘
- 각 데이터를 바로 크기를 기준으로 분류하므로 O(N)의 시간 복잡도를 가짐
- 데이터의 크기가 한정적일 때 사용할 수 있다
- MAX_VALUE 초과값은 정렬할 수 없다

### 계수정렬 구현  
> 0부터 10000까지 들어갈 수 있는 배열을 생성  
> 입력할 원소 개수를 입력하고 그만큼 for문을 돌려 값을 센다  
> 입력한 숫자 = 배열 인덱스. a[m]++ 해줘서 개수를 센다
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define MAX_VALUE 10001
// 10000보다 더 큰 값은 안됨

int n, m;
int a[MAX_VALUE];

int main(void) {
	
	scanf("%d", &n); // 입력할 원소개수
	for (int i = 0; i < n; i++) {
		scanf("%d", &m); 
		a[m]++;
	}

	for (int i = 0; i < MAX_VALUE; i++) {
		while (a[i] != 0) { 
			printf("%d ",i);
			a[i]--;
		}
	}
		
	system("pause");
	return 0;
}
```
# 기수정렬(Radix Sort)
- 자릿수를 기준으로 차례대로 데이터를 정렬하는 알고리즘
각 데이터를 자릿수를 기준으로 분류하므로 가장 큰 자릿수를 D라고 했을 때 O(DN)의 시간 복잡도를 가짐 
- 계수정렬보다 약간 더 느리지만, 숫자가 매우 큰 상황에서도 사용할 수 있다
 ### 기수정렬
 ``` c
 #define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define MAX 10000


void radixSort(int* a, int n) {
	int res[MAX], maxValue = 0;
	int exp = 1; // 자릿수
	for (int i = 0; i < n; i++) {
		if (a[i] > maxValue) maxValue = a[i]; //가장 큰 값을 먼저 구함
	}
	while (maxValue / exp > 0) {
		int bucket[10] = { 0 }; //자릿수 배열은 10개만 만들면됨 (0~9). 모든 값은 일단 0으로
		for (int i = 0; i < n; i++) bucket[a[i] / exp % 10]++; // 자릿수 배열처리
		for (int i = 1; i < 10; i++) bucket[i] += bucket[i - 1]; // 누적계산
		for (int i = n - 1; i >= 0; i--) { //같은 자릿수 끼리는 순서를 유지
			res[--bucket[a[i] / exp % 10]] = a[i];
		}
		for (int i = 0; i < n; i++) a[i] = res[i];
		exp *= 10;		
	}
}

int main(void) {
	
	int a[MAX];
	int i, n;
	scanf("%d", &n);
	for (i = 0; i < n; i++) {
		scanf("%d", &a[i]);
	}
	radixSort(a, n);
	for (i = 0; i < n; i++) {
		printf("%d ", a[i]);
	}
		
	system("pause");
	return 0;
}
 ```
 ---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]