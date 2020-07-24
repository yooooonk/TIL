# 세그먼트 트리 Segment Tree
-  여러 개의 데이터가 연속적으로 존재할 때 특정한 범위의 데이터의 합을 구하는 방법
- 선형적으로 구간 합 구하는 것은 비효율적 -> O(N)의 시간복잡도
- 트리 구조를 활용하여 구간 합을 구하는 과정은 O(logN)의 시간 복잡도를 가짐
    1. 완전 이진 트리에 데이터 삽입하기
    2. 트리 구조로 구간합 구하기 - 구간 합 트리 생성하기[특정 범위 인덱스 값을 저장]
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define NUMBER 7

int a[] = { 7,1,9,5,6,4,1 };
int tree[4 * NUMBER]; // 4를 곱하면 모든 범위를 커버할 수 있습니다

// start : 시작 인덱스, end : 끝 인덱스
int init(int start, int end, int node) {
	if (start == end) retrun tree[node] = a[start];
	int mid = (start + end) / 2;
	//재귀적으로 두 부분으로 나눈 뒤에 그 합을 자기 자신으로 합니다
	return tree[node] = init(start, mid, node * 2) + init(mid + 1, end, node * 2 + 1);
}

// start : 시작 인덱스, end : 끝 인덱스
// left, right : 구간 합을 구하고자 하는 범위
int sum(int start, int end, int node, int left, int right) {
	// 범위 밖에 있는 경우
	if (left > end || right < start) return 0;
	// 범위 안에 있는 경우
	if (left <= start && end <= right) return tree[node];
	// 그렇지 않다면 두 부분으로 나누어 합을 구하기
	int mid = (start + end) / 2;
	return sum(start, mid, node * 2, left, right) + sum(mid + 1, end, node * 2 + 1, left, right);
}

void update(int start, int end, int node, int index, int dif) {
	// 범위 밖에 있는 경우
	if (index<start || index>end) return;

	// 범위 안에 있으면 내려가며 다른 원소도 갱신
	tree[node] += dif;
	if (start == end) return;
	update(start, mid, node * 2, index, dif);
	update(mid + 1, end, node * 2 + 1, index, dif);
}

int main(void) {
	// 구간 합 트리의 인덱스를 제외하고는 모두 인덱스 0부터 시작
	// 구간 합 트리 생성하기
	init(0, NUMGER - 1, 1);

	//구간 합 구하기
	printf("0부터 6까지의 구간 합: %d\n", sum(0, NUMBER - 1, 1, 0, 6));
	
	// 구간 합 갱신하기
	printf("3부터 6까지의 구간 합: %d\n", sum(0, NUMGER - 1, 1, 3, 6));

	system("pause");

}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]