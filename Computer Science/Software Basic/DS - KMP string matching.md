# KMP 문자열 매칭

### 단순 비교 문자열 매칭

- 단순 비교 문자열 매칭 알고리즘은 두 문자열을 처음부터 끝가지 계속 비교하는 알고리즘 
- O(NM)의 시간 복잡도
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
