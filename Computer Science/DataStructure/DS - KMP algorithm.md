# 문자열 매칭

## 단순 비교 문자열 매칭

- 단순 비교 문자열 매칭 알고리즘은 두 문자열을 처음부터 끝가지 계속 비교하는 알고리즘 
- O(NM)의 시간 복잡도 = 비효율적
``` c
#include <string.h>
#include <stdio.h>

char* parent = "ABCDEFG";
char* pattern = "EF";

int main(void) {
	int parentSize = strlen(parent);
	int patternSize = strlen(pattern);
	for (int i = 0; i <= parentSize - patternSize; i++) {
		int found = 1;
		for (int j = 0; j < patternSize; j++) {
			if (parent[i + j] != pattern[j]) { found = 0; break; }
		}
		if (found) {
			printf("%d번째에서 찾았습니다.\n", i + 1);
		}
	}
	system("pause");
}
```

## KMP 문자열 매칭
- O(N+M)의 시간 복잡도
- 접두사와 접미사를 활용해 빠르게 문자열을 매칭할 수 있다
- 테이블 만들기
	1. pattern[j]와 pattern[i]가 일치하는지 반복적으로 확인. 
	2. 일치하는 경우 j에 1을 더한 뒤에 j의 인덱스를 table[i]에 삽입
	3. 불일치 하는 경우 j를 '마지막으로 일치했던 순간'까지의 인덱스(table[j-1])로 이동해 다시 검사.  
- 문자열 매칭
	1. 문자열 매칭을 진행할 때에도 불일치하는 경우 j를 '마지막으로 일치햇던 순간'까지의 인덱스(table[j-1])로 이동해 다시 검사
``` c
#include <string.h>
#include <stdio.h>

char* parent = "acabacdabac";
char* pattern = "abacdab";

//테이블 생성 함수 구현
int* makeTable(char* pattern) {
	int patternSize = strlen(pattern);
	int* table = (int*)malloc(sizeof(int) * patternSize);
	for (int i = 0; i < patternSize; i++) {
		table[i] = 0;
	}
	int j = 0;
	for (int i = 1; i < patternSize; i++) {
		while (j > 0 && pattern[i] != pattern[j]) {
			j = table[j - 1];
		}
		if (pattern[i] == pattern[j]) {
			table[i] = ++j;
		}
	}
	return table;
}

void KMP(char* parent, char* pattern) {
	int* table = makeTable(pattern);
	int parentSize = strlen(parent);
	int patternSize = strlen(pattern);
	int j = 0;
	for (int i = 0; i < parentSize; i++) {
		while (j > 0 && parent[i] != pattern[j]) {
			j = table[j - 1];
		}
		if (parent[i] == pattern[j]) {
			if (j == patternSize - 1) {
				printf("[인덱스 %d]에서 매칭 성공\n", i - patternSize + 2);
				j = table[j];
			}
			else{
				j++;
			}
		}
	}
}

int main(void) {
	KMP(parent, pattern);
	system("pause");
} 
```
---
__REFERENCE__
- fastcampus 컴퓨터 공학 전공 필수 [소프트웨어 베이직 - 나동빈]