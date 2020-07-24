# 인덱스 트리 Index Tree
- 세그먼트 트리는 구현하는 과정이 복잡하고 어렵다는 점에서 구간 합을 더 쉽게 구할 방법이 필요하다
- 인덱스 트리는 구현이 매우 간단하다
- 인덱스 트리를 활용해 구간 합을 구하는 과정도 O(logN)의 시간 복잡도를 가짐
- 인덱스 트리는 세그먼트 트리에 비해 메모리 효율성이 높다(왜?)
- 특정한 숫자의 마지막 비트 구하기(A & -A)
- 마지막 비트를 이용해 트리 구조 만들기 : 각 인덱스에 대하여 마지막 비트를 '내가 저장하고 있는 값들의 개수'로 계산
- 1부터 N까지 구간 합 구하기 : 마지막 비트만큼 구간을 앞으로 이동하며 합을 구한다
- 특정 인덱스 수정하기 : 마지막 비트만큼 구간을 뒤로 이동하며 값을 수정
``` c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#define NUMBER 7

int tree[NUMBER];

int sum(int i) {
	int res = 0;
	while (i > 0) {
		res += tree[i];
		// 마지막 비트만큼 빼면서 앞으로 이동
		i -= (i & -i);
	}
	return res;
}

void update(int i, int dif) {
	while (i <= NUMBER) {
		tree[i] += dif;
		// 마지막 비트만큼 더하면서 뒤로 이동
		i += (i & i - 1);
	}
}

// 구간 합 계산 함수
int getSection(int start, int end) {
	return sum(end) - sum(start - 1);
}



int main(void) {
	
	update(1, 7);
	update(2, 1);
	update(3, 9);
	update(4, 5);
	update(5, 6);
	update(6, 4);
	update(7, 1);
	printf("1부터 7까지의 구간 합: %d\n", getSection(1, 7));
	printf("인덱스 6의 원소를 +3만큼 수정\n");
	update(6, 3);
	printf("4부터 7까지의 구간 합: %d\n", getSection(4, 7));


	system("pause");

}
```

---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]