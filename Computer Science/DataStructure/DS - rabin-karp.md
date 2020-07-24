# 라빈카프 문자열 매칭 Rabin-Karp algorithm
- 아스키 코드 기반의 해시 함수를 이용하여 특정한 문자열에 대한 해시 값을 구함
- 라빈 카프 문자열 매칭 알고리즘에서 해시 함수는 '각 문자의 아스키 코드 값에 자리수에 해당하는 2의 제곱 수를 차례대로 곱하여 더한 값'을 구한다. 
- 일반적으로 서로 다른 문자열의 경우 일반적으로 해시 값이 다르게 나옴
- 같은 경우도 있어서 해시 충돌에 대한 처리가 필요. 해시 값이 일치하는 경우에만 문자열을 재검사
- 해시 함수를 반복적으로 계산할 때는 '문자열이 이어져 있다는 특징'을 이용하여 빠르게 계산한다
    - 다음 해시 값 = 2*(현재 해시 값 - 가장 앞에 있는 문자의 수치) + 새 문자의 수치
- 평균적으로 O(N+M)의 시간 복잡도를 가짐
- 상황에 따라 KMP알고리즘보다 빠르게 동작할수도 느리게 동작할 수도 있다
```c
#include <string.h>
#include <stdio.h>

char* parent = "acabacdabac";
char* pattern = "abacdab";

void check(char* parent, char* pattern, int start) {
	int found = 1;
	int patternSize = strlen(pattern);
	for (int i = 0; i < patternSize; i++) {
		if (parent[start + 1] != pattern[i]) {
			found = 0;
			break;
		 }
	}
	if (found) {
		printf("[인덱스 %d에서 매칭 발생]\n", start + 1);
	}
}

void rabinKarp(char* parent, char* pattern) {
	int parentSize = strlen(parent);
	int patternSize = strlen(pattern);
	int parentHash = 0, patternHash = 0, power = 1;
	for (int i = 0; i <= parentSize - patternSize; i++) {
		parentHash = parentHash + parent[patternSize - 1 - j] * power;
		patternhash = patternHash + pattern[patternSize - 1 - j] * power;
		if (j < patternSize - 1) power = power * 2; 
	}
}

int main(void) {
	rabinKarp(parent, pattern);
	system("pause");
}
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]