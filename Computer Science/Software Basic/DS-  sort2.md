# 퀵 정렬(Quick sort)
- 퀵 정렬이란 피벗을 기준으로 큰 값과 작은 값을 서로 교체하는 정렬기법
- 값을 서로 교체하는 데 N번, 엇갈린 경우 교체 이후에 원소가 반으로 나누어지므로 전체 원소를 나누는데 평균적으로 logN번이 소요되므로 평균적으로 O(NlogN)의 시간 복잡도를 가진다
- 원소를 절반식 나눌 때 logN의 시간 복잡도가 나오는 대표적인 예시는 완전 이진트리이다.
완전 이진트리 형태는 흔히 컴퓨터 공학에서 가장 선호하는 이상적인 형태이다

  

### 퀵 정렬 구현
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

void quickSort(int start, int end) {
	if (start >= end) return;
	int key = start, i=start + 1, j = end, temp;
	while (i <= j) { //엇갈릴 때까지 반복
		while (i <= end && a[i] <= a[key]) i++;
		while (j > start && a[j] >= a[key]) j--;
		if (i > j) swap(&a[key], &a[j]);
		else swap(&a[i], &a[j]);
	}
	quickSort(start, j - 1);
	quickSort(j+1 , end);
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
